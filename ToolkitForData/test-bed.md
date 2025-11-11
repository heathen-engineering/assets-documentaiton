# Test Bed

The **Test Bed** is our Unreal Engine 5.7 project where we are experimenting with the foundational systems for the Toolkit for Data. It is designed to explore and validate the core architecture that will power large-scale, emergent simulations while remaining highly efficient and designer-friendly.

{% hint style="info" %}
While the current R\&D is being conducted in Unreal Engine 5.7, using our live project as a testbed, the system is designed to be **engine-agnostic**. Heathen Engineering works across multiple engines, and all of our toolkits are fundamentally built to support this flexibility. For us, an engine is one tool among many in our kit, and the architecture is intended to allow integration with any engine in a consistent, high-performance way.
{% endhint %}

## Core Components

### DataStore

At the lowest level is **DataStore**, a native C++ data structure that serves as the CPU- and memory-sensitive foundation of the system. It is a **column-oriented, in-memory table** capable of managing heterogeneous data with **per-column stride**. DataStore supports both raw access for maximum performance and safe, bounds-checked access for stability.

**Key features of DataStore:**

* Column-oriented layout optimised for high-performance memory access
* Efficient read/write operations, including batch processing
* Safe and unchecked APIs for flexible usage
* Row-major serialisation for persistence or network transmission
* Thread-safe operations (planned for future extensions)

DataStore is designed as a **low-level foundation**, handling large-scale simulation data efficiently while giving higher-level systems the flexibility to reshape it for game systems.

### DataView

On top of DataStore sits **DataView**, an engine-specific, designer-friendly layer exposed to Blueprints. DataView’s responsibility is to **gather, transform, and present data** in formats that game systems expect while keeping the underlying DataStore highly optimised.

**Responsibilities of DataView:**

* Reading tightly managed DataStore data and mutating it into game-ready structures
* Writing back updates from game systems into the DataStore, maintaining optimised storage
* Exposing intuitive interfaces for designers and engineers
* Handling runtime data preparation without compromising real-time performance

### Mid-Level API / Subsystem

Bridging DataStore and DataView is the **mid-level API**, implemented as a Subsystem in Unreal. This layer:

* Creates and manages DataStores
* Coordinates batched reads and writes.
* Handles threaded access safely and efficiently
* Ensures usability while respecting performance and memory limits

This architecture allows **front-end systems to work with designer-friendly structures**, while the **back-end DataStore** operates with carefully tuned memory layouts optimised for CPU and memory efficiency.

## Purpose

The Test Bed is our **experimental proving ground**, enabling us to validate core systems, iterate on architecture, and refine the balance between performance, usability, and flexibility. By separating DataStore, DataView, and the mid-level API, we aim to deliver a toolkit capable of powering **emergent, large-scale simulations** that are both accessible and high-performance.
