# Introduction

{% hint style="success" %}
**Note: These tools are in preview**\
We follow a “dogfood” development approach—these tools are actively used and developed within our current WIP games. They are mature enough to share with our GitHub and Patreon supporters, so their documentation is provided here for early adopters.
{% endhint %}

## Data Lens Subsystem

**Data Lens** is an all-in-memory data store designed to manage large record sets (10s of thousands of records per table) in a memory-optimal, componentized format, enabling extremely fast select and update operations.

**Core Features**

* **Highly efficient in-memory storage:**\
  Uses compact, component-based layouts to minimise memory footprint while maximising cache efficiency for rapid data access and mutation.
* **Serialization-friendly:**\
  Tables and records are designed for straightforward, efficient serialisation, making full world state saving and loading performant and reliable.
* **Designer & modder friendly:**\
  Table definitions are driven by **Gameplay Tags**, enabling flexible, readable, and extensible schemas that are easily authored and extended.
* **Expression-driven queries:**\
  Supports a simple TSQL/Excel-style formula language to define computed columns and filters, accessible to designers without deep programming knowledge.
* **Debugging and inspection:**\
  Provides utilities to export tables as human-readable CSV-style data with headers and columns, aiding debugging and iterative design.
* **Parallel Processing:**\
  Orchestrates multi-threaded read/write and update operations, allowing real-time simulation of thousands of entities without blocking designer workflows.
* **Designer-friendly views:**\
  The DataLensTableView returns sorted, ready-to-use `TArray<Struct>` data defined by designers, abstracting complexity and enabling rapid iteration in Blueprints.

***

This subsystem is intended as the foundation for complex, persistent simulation environments, supporting real-time updates, large-scale AI state tracking, and rich designer control over gameplay data.

## Dialogue System Overview

The **Dialogue System** in the Toolkit provides a modular, designer-friendly foundation for creating dialogue interactions in-game. It is composed of two core base classes — one for logic (`UDialogueComponentBase`) and one for UI (`UDialogueWidgetBase`). Both are designed to be extended by designers in Blueprint to define individual dialogue scenarios without requiring C++ changes.

#### Core Principles

* **Boilerplate separation**: Common functionality (event wiring, state management, widget communication) is handled in C++. Designers only focus on the content and flow of a specific dialogue.
* **One Blueprint per dialogue**: Each unique dialogue is authored as its own `BP_DialogueComponent`, optionally with a paired `BP_DialogueWidget` if needed.
* **System-agnostic UI**: The base widget defines standard entry points (`OpenDialogue`, `UpdateDialogueText`) that can be implemented in UMG Blueprint to handle custom layouts or interaction logic.

#### Key Classes

* **`UDialogueComponentBase`**
  * Actor component to be added to NPCs or world objects.
  * Manages dialogue start/stop and calls into the widget.
  * Exposes `OnInteracted`, `OnDialogueStart`, and `OnDialogueEnd` events for Blueprint logic.
* **`UDialogueWidgetBase`**
  * Abstract widget class that receives dialogue updates.
  * Designed to be subclassed in UMG Blueprints.
  * Provides Blueprint-native `OpenDialogue` and `UpdateDialogueText` functions.

#### Designer Workflow

1. Create a new `BP_MyDialogueComponent` subclassing `UDialogueComponentBase`.
2. Create a matching `BP_MyDialogueWidget` subclassing `UDialogueWidgetBase`.
3. Implement dialogue flow and visuals using Blueprint logic.
4. Attach the component to an actor in your level or character.
