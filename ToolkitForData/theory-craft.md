# Theory Craft

When building a game data system, it helps to think in **layers**, from engine-agnostic core logic to designer-facing tools. Our current musings focus on the architecture that could support **DataLens / DataStore**, flexible enough to work in UE, Unity, or even other frameworks like O3DE, MonoGame, or MonoDevelop.

## Layers

***

### 1. **Native DataStore (Engine-Agnostic Core)**

**Purpose:** the true source of structured, high-performance game data, fully engine-independent.

**Characteristics:**

* Written in **pure C++** as a **column-oriented, in-memory store**.
* Supports **dynamic per-column stride**, raw byte storage, and flexible typed access.
* Provides both **unchecked raw access** for maximum performance and **safe, bounds-checked operations**.
* Stores arbitrary types, relationships, and traits through column metadata.
* Handles **serialisation** to and from row-major byte layouts efficiently.
* No dependencies on Unreal, Unity, or other engines.
* Acts as a **low-level API** for engineers to manipulate rows, columns, and values safely or directly.

**Core API Concepts (conceptual):**

```cpp
// Create an empty table with column metadata
DataStore store({ {4}, {8}, {16} }, 1024); // 3 columns, preallocate 1024 rows

// Raw access
store.SetRaw<int32_t>(row, col, value);
int32_t val = store.GetRaw<int32_t>(row, col);

// Safe access
bool ok = store.TrySet<float>(row, col, value);
float result;
ok = store.TryGet<float>(row, col, result);

// Serialization
std::vector<uint8_t> data = store.Dump();
store.LoadRaw(data);

// Column info
size_t rowStride = store.GetRowStride();
size_t rows = store.GetRowCount();
size_t cols = store.GetColumnCount();
size_t colStride = store.GetColumnStride(0);
```

**Why it exists:** all game logic and systems reference a single, high-performance “truth” without being tied to any engine. It allows other layers to build engine-specific APIs, DataViews, and designer tools while keeping the core logic fully portable and efficient.

***

### 2. **DataLens API (Engine-Native, Engineer-Facing)**

**Purpose:** the bridge between the **engine runtime** and the **engine-agnostic DataStore**.

**Characteristics:**

* Engine-specific (C++ in UE, C# in Unity, etc.) but **not designer-facing**.
* Handles:
  * Tick updates and payload buffers.
  * Threading and asynchronous updates.
  * Registering “tables” or “Actor Types.”
* Exposes an engineer-idiomatic API for interacting with the DataStore.
* Ensures **safe, performant engine integration**.
* Can feed data to engine-native systems such as AI, sensing, environment, or pathing without assuming specific designer workflows.

**Example in UE (conceptual):**

```cpp
class FDataLensEngineAPI {
public:
    void RegisterActorType(FName TypeName);
    void StageAttributeUpdate(FGuid RecordID, FName Attribute, int32 Value);
    void ProcessPayloads(); // Called by subsystem tick
};
```

**Example in Unity (conceptual):**

```csharp
public class DataLensAPI {
    public void RegisterActorType(string typeName);
    public void StageAttributeUpdate(Guid recordID, string attribute, object value);
    public void ProcessPayloads(); // Called via coroutine / Update loop
}
```

#### Double-Buffered Data Flow

The **DataLens layer** employs a **double-buffer system**, inspired by modern rendering pipelines, to maintain continuous real-time performance while avoiding thread contention or blocking reads.

Each **DataView** maintains two buffer pairs:

* **Data Buffers** — `ViewBuffer` (active) and `BackBuffer` (in preparation).\
  The `ViewBuffer` represents the most recent stable “frame” of view data, while the `BackBuffer` is asynchronously populated from `DataStores` based on the view’s _select_ expression.
* **Command Buffers** — `FrontCommandBuffer` (accepting new writes) and `BackCommandBuffer` (being processed).\
  Commands staged by the runtime or designer systems (writes, mutations, updates) are accumulated into the `FrontCommandBuffer` while the `BackCommandBuffer` is processed and applied to the underlying `DataStores`.

The **DataLens update cycle** runs independently from the engine’s render or tick rate and proceeds as follows:

1. **Select Phase:**\
   Each DataView executes its _select_ expression, reading from its mapped `DataStores` and writing results into its `BackBuffer`.
2. **Buffer Swap:**\
   When all views complete selection, `Data` and `Command` buffers are atomically swapped — the `BackBuffer` becomes the new active `ViewBuffer`, and the current `FrontCommandBuffer` becomes the new processing target.
3. **Command Phase:**\
   The DataLens layer aggregates and applies all staged updates from the swapped `CommandBuffers` to the relevant `DataStores`, resolving any conflicts or coalescing redundant updates.
4. **Repeat:**\
   The cycle repeats continuously at a configurable frequency (e.g. 30–60 Hz or adaptive), maintaining a consistent, up-to-date frame of world data for both C++ and Blueprint consumers.

This approach guarantees that:

* Designers and engineers always read from a **stable snapshot** of world data.
* Writers never block readers, ensuring deterministic read performance.
* The subsystem’s update rate can be tuned independently of the game frame rate for optimal scaling across hardware platforms (PC, console, cloud).

***

### 3. **DataView (Engine-Specific, Designer-Facing)**

**Purpose:** the designer’s bridge to runtime data, allowing **queries, outputs, and input** for game logic systems.

**Characteristics:**

* Fully engine-native and designer-accessible (Blueprints in UE, ScriptableObjects or MonoBehaviours in Unity).
* Can query **rows** from the DataStore via the API layer.
* Outputs to engine runtime systems:
  * AI Behaviour Trees
  * Senses such as vision or hearing
  * Environmental systems such as weather, triggers, or dynamic world effects
* Accepts inputs to stage updates back into the DataStore seamlessly.
* Flexible. The same DataView can drive multiple systems without hard-coded assumptions.

**Example in UE (conceptual Blueprint class):**

```cpp
UCLASS(BlueprintType)
class UDataView : public UObject {
    UFUNCTION(BlueprintCallable)
    FDataRow GetRow(FGuid RecordID);

    UFUNCTION(BlueprintCallable)
    void StageAttributeChange(FGuid RecordID, FName Attribute, int32 Value);
};
```

**Example in Unity (conceptual MonoBehaviour):**

```csharp
public class DataView : MonoBehaviour {
    public DataRow GetRow(Guid recordID);
    public void StageAttributeChange(Guid recordID, string attribute, object value);
}
```

***

## **Layer Relationships**

```
[ Designer / Blueprints or ScriptableObjects ] 
        <--> 
[ DataView (Designer-Facing) ] 
        <--> 
[ DataLens API Layer (Engineer-Facing) ] 
        <--> 
[ Native DataStore (Engine-Agnostic) ]
```

* **Native DataStore:** single source of truth, fully engine-independent.
* **DataLens API:** engine-specific, manages threading, ticks, buffers, and engine integration.
* **DataView:** designer-facing, flexible interface to query and update data, feeding multiple runtime systems.

***

### **Why this matters**

* The architecture separates **engine concerns**, **designer access**, and **core data logic**.
* Makes it possible to reuse the **same DataStore** across multiple engines.
* Enables complex, real-time systems such as AI, Senses, and environmental effects without engine lock-in.
* Keeps designer tooling simple and intuitive while giving engineers full control under the hood.
