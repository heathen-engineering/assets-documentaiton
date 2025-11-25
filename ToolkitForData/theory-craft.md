# Theory Craft

When building a game data system, it helps to think in layers, from engine-agnostic core logic to designer-facing tools. DataLens is designed to support large-scale emergent simulations across engines (UE, Unity, etc.), while maintaining high memory and CPU efficiency.

## Layers

***

### 1. **Native DataStore (Engine-Agnostic Core)**

**Purpose:** the true source of structured, high-performance game data, fully engine-independent.

**Characteristics:**

* Written in pure C++ as a column-oriented, in-memory store.
* Supports dynamic per-column stride, raw byte storage, and flexible typed access.
* Provides both unchecked raw access for maximum performance and safe, bounds-checked operations.
* Stores arbitrary types, relationships, and traits through column metadata.
* Handles serialisation to and from row-major layouts efficiently.
* No dependencies on Unreal, Unity, or other engines.
* Acts as a low-level API for engineers to manipulate rows, columns, and values safely or directly.

**Why it exists:** All systems reference a dense, engine-agnostic “truth” that maximises storage efficiency. This allows other layers to build engine-specific APIs and designer-facing tools without duplicating the data.

**Core API Concepts (conceptual):**

```cpp
DataStore store({ {4}, {8}, {16} }, 1024); // 3 columns, preallocate 1024 rows
store.SetRaw<int32_t>(row, col, value);
int32_t val = store.GetRaw<int32_t>(row, col);
```

Serialization, column info, and safe access remain fully supported.

***

### 2. **DataLens API (Engine-Native, Engineer-Facing)**

**Purpose:** the bridge between the **engine runtime** and the **engine-agnostic DataStore**.

**Characteristics:**

* Engine-specific (C++ in UE, C# in Unity) but engineer-facing, not designer-facing.
* Handles tick updates, staged updates, threading, and asynchronous orchestration.
* Manages registration of “tables” or actor types and provides idiomatic APIs for safe DataStore interaction.

**Updated Note:** Double-buffering for DataViews was explored but found unfeasible under Phase 1 constraints. Each DataView is now treated as a cached, independent row-major representation. DataLens orchestrates these views per tick, leaving overlapping or conflicting caches as a developer-managed concern.

***

### 3. **DataView (Engine-Specific, Designer-Facing)**

**Purpose:**\
Provides filtered, row-major slices of data for game logic, with read/write access to support gameplay systems.

**Characteristics:**

* Scoped, ephemeral cache: Each DataView is a materialised row-major representation derived from one or more DataStores.
* Context-sensitive: Only aggregates data when needed by game systems; not precomputed for all actors.
* Orchestration: DataLens updates registered views per tick; developers manage conflicts between overlapping views.
* Supports queries, joins, and calculated columns.

**New Actor Knowledge Model (Experimental):**

* Each actor may have a scoped, imperfect “view” of the simulation state.
* Actor knowledge stores reference canonical DataStores and store metadata such as confidence, belief strength, acquisition method (observed/derived/rumour), and temporal decay.
* DataViews aggregate relevant actor- or topic-specific data for gameplay systems without materialising every possible state.

***

### 4. DataSystem (Engine-Specific, Designer-Facing)

**Purpose:**\
Provides column-oriented, system-level updates across subsets of the world.

**Characteristics:**

* Engine-native and designer-friendly.
* Bufferless, operating immediately after DataView updates.
* Suitable for recurring computations, aggregations, or status updates that do not require per-record derived data.
* Frequency-driven: Updates run at configurable intervals (frame, 10 Hz, 1 Hz).

**Example Usage:**

* Hunger, fatigue, or energy decay.
* Health or mana regeneration.
* Environmental effects, automated resource production, crowd or faction adjustments.

***

## **Layer Relationships**

```
[ Designer / Blueprints or ScriptableObjects ] 
        <--> 
[ DataView & DataSystem (Designer-Facing) ] 
        <--> 
[ DataLens API Layer (Engineer-Facing) ] 
        <--> 
[ Native DataStore (Engine-Agnostic) ]
```

* **Native DataStore:** single source of truth, fully engine-independent.
* **DataLens API:** engine-specific, manages threading, ticks, buffers, and engine integration.
* **DataView & DataSystem:** designer-facing, flexible interface to query and update data, feeding multiple runtime systems.

***

### **Why this matters**

* The architecture separates **engine concerns**, **designer access**, and **core data logic**.
* Makes it possible to reuse the **same DataStore** across multiple engines.
* Enables complex, real-time systems such as AI, Senses, and environmental effects without engine lock-in.
* Keeps designer tooling simple and intuitive while giving engineers full control under the hood.

## Speculative Game System Design

This section explores how a massive-world RPG might leverage the DataLens system to solve real design challenges. It draws on Heathen’s own game designs and serves as a practical “dog food” proof of concept for DataLens. Here we demonstrate **how DataLens could support both small-scale narrative experiments and large-scale, multi-system RPGs**, validating the system’s ability to manage scoped knowledge, actor autonomy, and emergent events in real-time.

***

### [Túatha Echoes: The Barrow](https://app.gitbook.com/o/NeMTNjC4USdRjoSZy6E7/s/gzmKuI14tHw48YsinkIN/)

A small, linear narrative visual novel-style game introducing players to the world’s concepts of life, death, and cyclical existence. The player assumes the role of a fatally wounded hunter transitioning from life to death.

**Gameplay Context:**

* The Barrow functions as a hospital, hospice, temple, school, and burial space.
* As the player transitions, their perception changes: actors, events, and interactions become contextually dependent on their state.
* The player chooses an “afterlife” path through interaction with necromancers, spirits, artefacts, and unfolding events.

**DataLens Application:**

* Emergent dialogues and interactions are driven by DataLens-defined scopes of knowledge.
* “World Data” is defined for each potential path:
  * Marvir Child (reborn as a spirit)
  * Lich Adherent (sacred calling)
  * Apprentice (linger to aid the Barrow)
  * Spirit Lantern (bound to the world differently)
  * Go Beyond (unknown fate)
* Player observations (e.g., a birth, a funeral, ancestral spirits) feed into DataLens, dynamically shaping what knowledge, actors, and dialogue options are accessible.
* DataLens effectively manages the scope of the player’s knowledge, informing which interactions are valid, which events can be perceived, and which conversational options are presented.

***

### [Túatha: The Oirirc Saga – Shattered](https://app.gitbook.com/o/NeMTNjC4USdRjoSZy6E7/s/xmAptAznllHoOMbGHvvQ/)

The first entry in a planned trilogy, a primarily linear narrative RPG following the player through the death of innocence via trauma, discovery of the wider world, and the selection and commitment to a life path (becoming a Heathen / Gallowglass).

**Gameplay Context:**

* Player interactions with NPCs, events, and environments have a minor but meaningful influence on the world’s evolution.
* Emergent variability is achieved while maintaining narrative structure.

**DataLens Application:**

* DataLens defines the environment, events, and actor states.
* Actors simulate semi-autonomously, allowing player influence and randomness while generally converging on the intended story beats.
* DataLens supports subsystems including economy, factions, and villages, maintaining simulation state consistency and performance.
