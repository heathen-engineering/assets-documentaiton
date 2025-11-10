# Data Lens Table

{% hint style="success" %}
**Note: These tools are in preview**\
We follow a “dogfood” development approach—these tools are actively used and developed within our current WIP games. They are mature enough to share with our GitHub and Patreon supporters, so their documentation is provided here for early adopters.
{% endhint %}

The _Data Lens Table_ is the core structure behind our emergent simulation framework — a unified data source used to model everything from NPCs and mobs to factions, villages, and districts. While currently visible and used directly for development and testing, the long-term plan is for it to become a _behind-the-scenes construct_, accessible only through the Data Lens Subsystem and its `IProcessor`s.

What matters most now is the **shape of the data**, as it defines what the system _can_ and _cannot_ do. Here’s a breakdown of the core features:

### **ID**

Every record in a table is assigned a unique `ID`, which allows other records to reference it _directly_, independent of row index or table position. This makes insertions and deletions safe and enables flexible, dynamic record relationships.

### **Attributes**

`Attributes` are `int32` scalar values used to store basic data like health, level, rank, or currency. We don’t use floats for precision reasons — instead, precision is handled via queries. For example, 100 HP with two decimal points of precision would be stored as `10000`. The system then divides appropriately when presenting the value. This ensures fast, stable maths and eliminates float drift in critical simulations.

### **Related Records**

This is an array of `FRecordAddress` structs, allowing each record to reference _any number of other records_, across types and tables. This is the mechanism for modelling relationships like family ties, faction memberships, debts, rivalries, etc. Importantly, these relationships are _record-local_, meaning each record maintains its own perspective of the relation.

### **Traits**

Traits are powered by Unreal’s `FGameplayTagContainer`, providing a flexible, set-based tagging system to define what a record “is” — e.g. its class, race, skills, roles, or states. This supports fast queries and layered systems built on well-understood gameplay tag principles.

***

## Working With Table Data

Tables are not accessed directly; instead, all interactions go through the Subsystem. This design allows the Subsystem to orchestrate reads, writes, and updates in a controlled manner—ensuring views always reflect the latest data while minimising impact on the main thread.

### Read

To read table data you need to use a Data Lens Table View. With a view in place you can read its records at any time via the Get View Results node

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### Write

To write to a table, you use the table's tag and call the appropriate function on the Data Lens Subsystem.&#x20;

{% hint style="info" %}
These operations are not executed instantly; rather, they are collected and batched and executed on the next "Tick" of the Subsystem. These functions can be safely called at any time from any system, the Data Lens Subsystem will orchestrate the actual application of these commands to the related tables.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

***

## Defining Tables via Gameplay Tags

### Root Category: `DataRecords`

* **Purpose**: Every table in Data Lens must be rooted under the single, top‐level tag `DataRecords`.
*   **Usage**: When the Subsystem runs `InitializeEmptyDatabase()`, it calls

    ```cpp
    cppCopyEditFGameplayTag RootTag = FGameplayTag::RequestGameplayTag(FName("DataRecords"));
    FGameplayTagContainer Children = UGameplayTagsManager::Get().RequestGameplayTagChildren(RootTag);
    ```

    This returns all direct children of `DataRecords`. Each child tag is treated as one table.
*   **Example**:

    ```
    mathematicaCopyEditDataRecords.NPC
    DataRecords.Item
    DataRecords.Weapon
    DataRecords.DialogueLine
    ```

    In this example, four tables (“NPC,” “Item,” “Weapon,” “DialogueLine”) will be automatically created at runtime.

***

### Attribute Subcategory: `Att`

* **Location**: For each table tag `<TableTag> = DataRecords.<TableName>`, all attribute columns must live under a sub‐tag called `Att`.
*   **Naming Convention**:

    ```
    php-templateCopyEditDataRecords.<TableName>.Att.<AttributeName>
    ```

    * `<TableName>` is exactly the name of the table (the child under `DataRecords`).
    * `Att` is a literal token telling the Subsystem to treat its children as “attribute” columns.
    * `<AttributeName>` is the leaf name for that column.
* **Discovery**:
  1. The Subsystem sees `DataRecords.<TableName>` as a table.
  2. It then calls `RequestGameplayTagChildren(DataRecords.<TableName>)` to find all immediate subtags—one of which should be `Att`.
  3. It calls `RequestGameplayTagChildren(DataRecords.<TableName>.Att)` to enumerate all `<AttributeName>` tags.
  4. Each `DataRecords.<TableName>.Att.<AttributeName>` becomes one integer‐typed column in `UDataLensTable`.
*   **Example**:

    ```
    mathematicaCopyEditDataRecords.NPC.Att.Health
    DataRecords.NPC.Att.Mana
    DataRecords.NPC.Att.Level
    DataRecords.NPC.Att.FactionID
    ```

    The “NPC” table will have four attribute columns:

    * “Health” (stored as an `int32` per record),
    * “Mana,”
    * “Level,”
    * “FactionID.”

***

### Related‐Records Subcategory: `Ref`

* **Location**: Similarly, for each table tag `DataRecords.<TableName>`, any column that stores references to other records goes under a sub‐tag `Ref`.
*   **Naming Convention**:

    ```
    php-templateCopyEditDataRecords.<TableName>.Ref.<RelatedColumnName>
    ```

    * `Ref` is a literal token indicating “this column holds an array of FRecordAddress.”
    * `<RelatedColumnName>` is the name of that related‐records column.
* **Discovery**:
  1. The Subsystem sees `DataRecords.<TableName>`.
  2. It calls `RequestGameplayTagChildren(DataRecords.<TableName>)` to find `Ref`.
  3. It calls `RequestGameplayTagChildren(DataRecords.<TableName>.Ref)` to enumerate all `<RelatedColumnName>` tags.
  4. Each `DataRecords.<TableName>.Ref.<RelatedColumnName>` becomes one “related‐records” field (an array of `FRecordAddress`) in `UDataLensTable`.
*   **Example**:

    ```
    pgsqlCopyEditDataRecords.NPC.Ref.Friends
    DataRecords.NPC.Ref.InventoryItems
    DataRecords.NPC.Ref.QuestGivers
    ```

    The “NPC” table will have three related‐records columns:

    * “Friends” (an array of addresses pointing to other NPC records),
    * “InventoryItems” (addresses of records in an “Item” table),
    * “QuestGivers” (addresses in a “Quest” table).

***

### Complete Tag Tree Example

Imagine you need two tables—“NPC” and “Item”—each with both attributes and related‐records. You would author tags like:

```
pgsqlCopyEditDataRecords
├── NPC
│   ├── Att
│   │   ├── Health
│   │   ├── Mana
│   │   ├── Level
│   │   └── FactionID
│   └── Ref
│       ├── Friends
│       └── InventoryItems
└── Item
    ├── Att
    │   ├── Value
    │   ├── Weight
    │   └── Rarity
    └── Ref
        ├── CraftedBy    (addresses into a “Recipe” table, if it exists)
        └── LootedFrom   (addresses into “NPC” or “Chest” tables)
```

* **Initialization**:
  * `InitializeEmptyDatabase()` sees two top‐level children under `DataRecords`:
    1. `DataRecords.NPC` → creates a `UDataLensTable` instance keyed under `FGameplayTag(“DataRecords.NPC”)`.
    2. `DataRecords.Item` → creates a second `UDataLensTable` under `FGameplayTag(“DataRecords.Item”)`.
  * For “NPC” table it finds four attribute tags (`Health`, `Mana`, `Level`, `FactionID`) and two related tags (`Friends`, `InventoryItems`). It builds its internal arrays accordingly.
  * For “Item” table it finds three attribute tags (`Value`, `Weight`, `Rarity`) and two related tags (`CraftedBy`, `LootedFrom`).

***

### Key Benefits & “Why This Matters”

1. **Designer/Modder‐Friendly**
   * Anyone can add a brand‐new table simply by dropping a new tag under “DataRecords.” No C++ recompilation necessary—just update your `.ini` or your Tag list and run.
   * Adding or removing columns is equally trivial: designers create or delete tags under `… .Att.` or `… .Ref.`.
2. **Predictable Schema Assumptions**
   * We guarantee that each table’s “attributes” are laid out in a dense `TArray<int32>` whose indices exactly match the order of tags under `… .Att`.
   * Likewise, each table’s “related‐records” are stored as a `TArray<TArray<FRecordAddress>>` whose indices match `… .Ref.` tags.
   * Because the Subsystem scans the entire hierarchy once at startup, it can pre‐allocate any needed arrays and maintain perfect index alignment—no hash lookups at runtime, only O(1) by‐index access.
3. **Automatic Updates & Version Tolerance**
   * If a saved game holds an older or newer set of tags—perhaps modders added or removed columns—the load logic (in `LoadTable()`) will:
     1. Build a mapping from “live” AttributeTags to “saved” AttributeTags, filling missing columns with zeros.
     2. Build a mapping for RelatedTags, filling missing arrays as empty.
     3. Drop any unknown tags present in the save that no longer exist under the current `DataRecords` hierarchy (and log a warning).
4. **Fast, In‐Memory Structure‐of‐Arrays Layout**
   *   Because every table’s “columns” are pre‐known and size‐fixed, each `UDataLensTable` is effectively a “gameplay‐tag‐indexed” SoA database:

       ```cpp
       cppCopyEditTArray<FGuid> IDs;                   // record GUIDs
       TArray<FRecordAttributeValues> Attributes;       // each holds an array of int32, aligned to Att tags
       TArray<FRecordRelatedAddresses> RelatedRecords;   // each holds arrays of FRecordAddress, aligned to Ref tags
       TArray<FGameplayTagContainer> Traits;            // per‐record trait tags
       ```
   * Lookups by tag (e.g. “find the index for DataRecords.NPC.Att.Health”) happen once at initialization. From that point forward, setting/getting any attribute or related‐record is simply a matter of indexing into a known array.

***

### Summary of Steps to “Create” a New Table

1. **Author Tags**
   *   In your project’s Tag definitions (e.g. in `DefaultGameplayTags.ini` or via the Tag Editor), add:

       ```
       cppCopyEdit+GameplayTagTable=(TagName="DataRecords.NPC")
       +GameplayTagTable=(TagName="DataRecords.NPC.Att.Health")
       +GameplayTagTable=(TagName="DataRecords.NPC.Att.Mana")
       +GameplayTagTable=(TagName="DataRecords.NPC.Ref.Friends")
       // … etc.
       ```
2. **Subsystem Initialization**
   *   At runtime (usually during your GameInstance or early startup), call:

       ```cpp
       cppCopyEditUDataLensSubsystem::GetDataLensSubsystem()->InitializeEmptyDatabase();
       ```
   * The Subsystem will:
     1. Enumerate all direct children of `DataRecords.*` → create one `UDataLensTable` object per child.
     2. For each new `UDataLensTable`, read `… .Att.*` to build its attribute‐columns, and `… .Ref.*` to build its related‐records columns.
3. **Now You Have a “Live” Table**
   * Throughout gameplay, you can query table size, read attributes/relations, or stage writes (via payloads) by referencing these same tags.
   *   Example Blueprint:

       ```
       textCopyEditSetAttribute(RecordID=SomeGUID,
                    Attribute=GameplayTag("DataRecords.NPC.Att.Health"),
                    Value=75);
       ```
   * The Subsystem infers that “Health” belongs to table `DataRecords.NPC` and therefore routes that payload into the correct `UDataLensTable`.

***

By following these conventions—placing every table under `DataRecords`, grouping all attributes under `.Att.`, and all related‐records under `.Ref.`—we achieve:

* **Zero‐code table creation** (just add tags).
* **Automatic, index‐aligned column management** (no runtime string lookups).
* **Full modder/designer flexibility**, since the Subsystem simply “reacts” to whatever tags exist under `DataRecords` at startup.

This setup is the foundation for everything else (querying via Views, batching writes, serializing to disk, etc.), ensuring both performance and ease of iteration for large‐scale narrative or simulation systems.
