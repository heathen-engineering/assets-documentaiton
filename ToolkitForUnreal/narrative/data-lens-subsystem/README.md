# Data Lens Subsystem

{% hint style="success" %}
**Note: These tools are in preview**\
We follow a “dogfood” development approach—these tools are actively used and developed within our current WIP games. They are mature enough to share with our GitHub and Patreon supporters, so their documentation is provided here for early adopters.
{% endhint %}

The **Data Lens Subsystem** is our in-memory data orchestration core, designed for large-scale, simulation-heavy games (think Radiant AI, Nemesis, or The Sims). It manages all `UDataLensTable` instances and provides:

* A **tag-driven schema**, so designers (and modders) define “tables” via Gameplay Tags (e.g. `DataRecords.NPC.Att.Health`, `DataRecords.NPC.Ref.Friends`).
* **High-performance, SoA-style storage** for millions of records in RAM, with fast, parallelizable queries.
* A **payload-driven write buffer**, which batches and threads safety checks every create/update/delete operation.
* **Hot “views”** that automatically churn and update designer-defined USTRUCTs (via `UDataLensTableView`) at a configurable frequency (default 10 Hz).

By handling all reads (Gather) and writes (Write) on separate threads, with a lightweight “Commit” sync on the main thread, the Subsystem can support mass NPC or entity simulations entirely in Blueprint or C++ without bespoke per-record logic.

***

## Core Responsibilities

### **Initialization & Lifecycle**

* **`Initialize(…)`**\
  • Constructs every `UDataLensTable` based on all child tags under `DataRecords.*`.\
  • Resets both payload buffers (A/B) so designers can immediately begin writing and querying.
* **`Deinitialize()`**\
  • Destroys all tables, releases memory.

### **Singleton Access**

* **`GetDataLensSubsystem()`**\
  • Blueprint‐ and C++‐friendly static getter.

### **Tag-Driven Schema**

* **Tables = Gameplay Tags**\
  • A “table” is defined by a Gameplay Tag like `DataRecords.NPC`.\
  • Attribute columns under `… .Att.*` and Related columns under `… .Ref.*` drive each table’s internal arrays.
* **Modder-Friendly**\
  • Adding tags in the `DataRecords` hierarchy automatically defines new tables or columns at runtime.\
  • On Load, we reconcile saved tags with current schema: any unknown tags are logged and dropped.

### **View Management**

* **`RegisterView(UClass* ViewType)`**\
  • Registers a `UDataLensTableView` subclass so it can be churned automatically.
* **`GetView(…)`**\
  • Returns the active instance of that view for Blueprint consumption.
* **Hot Churn & Commit**\
  • Every tick (≈100 ms by default), the Subsystem:
  1. \*\*Gather/\*\*_Churn_ – Launches each registered view’s `Churn()` on worker threads.
  2. **Commit** – Once all `Churn()` calls finish, it calls `Commit()` (main thread) so each view’s `RawDataBuffer` is guaranteed consistent and ready for immediate Blueprint reads.
  3. **Broadcast** – Raises `OnUpdated(float CycleDuration)` so systems can react.

### **Payload-Driven Writes**

Reads and Writes happen asynchroniously on background threads, the Data Lens Subsystem orchastrates this by "Churning" views on background threads and refreshing the "Snapshot" that is always available to the main thread. Similarly thoguh in reverse the "Writer" functions of the Data Lens Subsystem:

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Are compiled and batched on the main thread into a "Payload Buffer" meaning you can freely send update/write commands at will and the system will organize thouse making them ready for the threads to process on the next tick.

* **Dual‐Buffer Design (A/B)**\
  • **Writable\_PayloadBuffer** (A or B) accumulates any `SetAttribute`, `AddRelatedAddress`, `CreateNewRecord`, etc., from Blueprints or C++.\
  • **Readable\_PayloadBuffer** holds the previous frame’s snapshot, safe for threaded writes.\
  • On each cycle, the Subsystem swaps (A⇄B) pointers, then processes `Readable\_PayloadBuffer` in parallel, applying updates to `UDataLensTable` instances.
*   **`FDataLensRecordUpdatePayload`** holds all staged operations for a single record:

    ```cpp
    cppCopyEditstruct FDataLensRecordUpdatePayload
    {
        FGuid                   RecordID;
        TMap<int32,int32>       AttributesToSet;    // column‐index → value
        TMap<int32,TArray<FRecordAddress>> RelatedToAdd, RelatedToRemove;
        TSet<int32>             ClearRelated;       // column indices to reset
        FGameplayTagContainer   TraitsToAdd, TraitsToRemove;
        bool                    bClearTraits = false;
        bool                    bClearTable  = false;
        bool                    bDeleteRecord = false;
    };
    ```
* **Buffered Write Workflow**
  1. **During gameplay**: any call like\
     `SetAttribute(FGuid, FGameplayTag, int32)`,\
     `AddRelatedAddress(...)`,\
     `CreateNewRecord(DataRecords.MyTable)`, etc.,\
     simply finds or creates that record’s `FDataLensRecordUpdatePayload` inside `Writable_PayloadBuffer[TableTag][RecordID]` and merges changes (overwriting, cancelling, or clearing as needed).
  2. **At the end of each cycle** (after all views commit), the Subsystem
     * Swaps A⇄B so the previous frame’s writes become “readable.”
     * Launches one worker thread per table to iterate its payload map and call each table’s `ApplyPayload(...)`.
     * Once all payloads apply, it clears `Readable_PayloadBuffer` so the next writes from Blueprints go into the other buffer.

### **Serialisation & Save/Load**

*   **`SaveDatabase()`** returns a `FDataLensDatabaseSaveData` (BlueprintType) which contains an array of `FDataLensTableSaveData` for each table. Each table’s saved struct holds:

    ```cpp
    USTRUCT(BlueprintType)
    struct FDataLensTableSaveData
    {
        GENERATED_BODY()

        UPROPERTY() FGameplayTag  TableTag;        // e.g. DataRecords.MyTable
        UPROPERTY() TArray<FGuid>    IDs;
        UPROPERTY() TArray<FGameplayTag>    AttributeTags;
        UPROPERTY() TArray<FGameplayTag>    RelationTags;
        UPROPERTY() TArray<FRecordAttributeValues>    Attributes;
        UPROPERTY() TArray<FRecordRelatedAddresses>    RelatedRecords;
        UPROPERTY() TArray<FGameplayTagContainer>      Traits;
    };
    ```
* **`LoadDatabase(const FDataLensDatabaseSaveData&)`**\
  • Reinitializes all tables from scratch, then for each saved table:
  1. Builds a fresh empty `UDataLensTable` based on the current schema.
  2. Maps saved columns → current columns by tag. Missing columns default to zero/empty; extras are logged/ignored.
  3. Populates `IDs`, attribute arrays, related arrays, and trait containers in index-aligned order.

***

## Workflow & Threading

The Data Lens Subsystem threads the churn of views and buffers the application of table update commands. The net result is view results are always available and always safe on the main thread with minimal impact to the main thread. While in the background, the system constantly applies incoming update commands and updates the view's results accordingly.

The Data Lens Subsystem consequently runs in its own update loop, independent from the rest of the engine. This remains transparent to designers as the system syncs results via the Views and buffers commands via the Writer tools. You can adjust the frequency the Data Lens Subsystem processes on easily:

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

The System Frequency defaults to 10Hz aka 10 times a second, the system may take longer than that to "Tick" but will never be faster than the frequency you set.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

You can optionally listen on the Updated event of the Data Lens Subsystem which will fire each time a Tick is completed and will report the duration that tick took to complete.

***

## Public Blueprint/C++ API

1.  **Initialization & Tables**

    ```cpp
    UFUNCTION(BlueprintCallable, Category="DataLens")
    void InitializeEmptyDatabase();

    UFUNCTION(BlueprintCallable, Category="DataLens")
    UDataLensTable* GetDataTable(FGameplayTag TableTag) const;
    ```

    * After calling `InitializeEmptyDatabase()`, every “child” of `DataRecords.*` is a fresh, empty `UDataLensTable`.
2.  **Views**

    ```cpp
    UFUNCTION(BlueprintCallable, Category="DataLens")
    void RegisterView(TSubclassOf<UDataLensTableView> ViewType);

    UFUNCTION(BlueprintCallable, Category="DataLens")
    UDataLensTableView* GetView(TSubclassOf<UDataLensTableView> ViewType);
    ```

    * Once a view class is registered, its single instance will be automatically churned every cycle.
    * Blueprint nodes can call `GetView(...)->GetResults()` to receive a `TArray<TheirStruct>` at any time (always safe on the main thread).
3.  **Writes (Payload Builders)**

    ```cpp
    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void SetAttribute(FGuid RecordId, FGameplayTag AttributeTag, int32 Value);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void AddRelatedAddress(FGuid RecordId, FGameplayTag RelatedTag, FRecordAddress Address);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void RemoveRelatedAddress(FGuid RecordId, FGameplayTag RelatedTag, FRecordAddress Address);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void ClearRelatedAddresses(FGuid RecordId, FGameplayTag RelatedTag);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void AddTraitTag(FGuid RecordId, FGameplayTag TableTag, FGameplayTag TraitTag);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void RemoveTraitTag(FGuid RecordId, FGameplayTag TableTag, FGameplayTag TraitTag);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void ClearTraitTags(FGuid RecordId, FGameplayTag TableTag);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    FGuid CreateNewRecord(FGameplayTag TableTag);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void DeleteRecord(FGuid RecordId, FGameplayTag TableTag);

    UFUNCTION(BlueprintCallable, Category="DataLens|Writer")
    void EmptyTable(FGameplayTag TableTag);
    ```

    * Each call simply stages an operation in the **writable payload buffer**—no immediate table mutation.
    * All pending payloads are applied in bulk at the start of the next cycle’s **Payload Processing** phase.
4.  **Save/Load**

    ```cpp
    UFUNCTION(BlueprintCallable, Category="DataLens|SaveLoad")
    FDataLensDatabaseSaveData SaveDatabase();

    UFUNCTION(BlueprintCallable, Category="DataLens|SaveLoad")
    void LoadDatabase(const FDataLensDatabaseSaveData& SaveData);
    ```

    * **SaveDatabase()** returns a self-contained data struct capturing every table’s `IDs`, `AttributeTags`, `RelationTags`, `Attributes`, `RelatedRecords`, and `Traits`.
    * **LoadDatabase(...)** rebuilds each table from its save data, mapping old columns to the current schema and filling gaps or ignoring extras as needed.

***

## Architecture Notes & Roadmap

* **Fully In-Memory, Serializable Store**\
  • Tables are kept entirely in RAM in a Structure-of-Arrays layout, ensuring fast, cache-friendly reads and writes.\
  • All tables (and their data) can be saved or loaded via `SaveDatabase()` / `LoadDatabase()`, producing a self-contained, tag-driven snapshot that designers or save systems can persist without thread-conflicts.
* **Tag-Driven Design**\
  • Each table is defined by a Gameplay Tag (e.g. `DataRecords.NPC`). All attribute columns live under `… .Att.*`, and all related-record columns under `… .Ref.*`.\
  • Modders or designers can add new tables or columns simply by adding tags underneath `DataRecords.`—the Subsystem picks these up at runtime when you call `InitializeEmptyDatabase()`.\
  • On Load, we reconcile saved columns with the current tag hierarchy: any unknown/missing columns default to zero or empty, and extras are logged and dropped.
*   **Hot Views & Constant Loop**\
    We maintain a repeating asynchronous loop (throttled to \~10 Hz by default) that alternates between two phases:

    1. **Payload Processing (Writes)**\
       • Swap the read/write buffers.\
       • For each table with pending record-update payloads, dispatch a worker thread that applies every `FDataLensRecordUpdatePayload` to its `UDataLensTable` via `ApplyPayload(…)`.\
       • Once _all_ table-write tasks complete, the buffer is cleared and ready to accumulate new writes. Immediately proceed to “View Churn.”
    2. **View Churn & Commit (Reads)**\
       • Dispatch a worker thread for each registered `UDataLensTableView` that runs its `Churn()`, building intermediate row data off the latest tables.\
       • Once _all_ `Churn()` tasks finish, switch to the main thread and call each view’s `Commit()`, making their `RawDataBuffer` safe for instant Blueprint or C++ reads.\
       • Broadcast `OnUpdated(float CycleTime)` to report how long the complete write→churn→commit cycle took, then loop back to “Payload Processing.”

    Because the entire loop is fully asynchronous and thread-safe, the Subsystem can handle tens (or hundreds) of thousands of records at \~10 Hz (or faster if configured), without blocking the game thread.
* **Blueprint Integration & Safe-Failing**\
  All common table- and record-manipulation functions (e.g. `SetAttribute()`, `CreateNewRecord()`, `AddRelatedAddress()`, etc.) are BlueprintCallable. Each call stages a payload—there is no immediate table mutation. If a designer references a nonexistent table or column, we log a warning instead of crashing. This ensures modder-friendly iteration during development and shipping.

***

**Key Takeaways:**

* We no longer plan an explicit `IProcessor` interface—our constant loop (Payload → View → Payload) already cleanly separates read vs. write phases, fully parallelized per table or per view.
* Future enhancements may include:\
  • **Per-Column Indexes** to accelerate “WHERE” or “GROUP BY” logic inside views (e.g. instantly “All NPCs whose Faction = X”).\
  • **Dirty-Flag or Event-Driven Triggers** so that, rather than a fixed 10 Hz, only tables or views whose underlying data actually changed get churned, further reducing CPU load.\
  • **Blueprint-Exposed Throttling** so designers can dial up or down the update frequency at runtime.

By layering these optimisations on top of our current constant, asynchronous write → read cycle, the Data Lens Subsystem becomes a robust, designer-friendly core for mass data simulation in open-world or emergent-behaviour games.
