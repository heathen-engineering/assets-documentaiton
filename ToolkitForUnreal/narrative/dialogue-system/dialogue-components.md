# Dialogue Components

{% hint style="success" %}
**Note: These tools are in preview**\
We follow a “dogfood” development approach—these tools are actively used and developed within our current WIP games. They are mature enough to share with our GitHub and Patreon supporters, so their documentation is provided here for early adopters.
{% endhint %}

The **Dialogue Component** is the core engine of the Dialogue System, built to give designers full control over dialogue logic using familiar Unreal Engine workflows. It is an `ActorComponent` designed to be subclassed in Blueprint or C++, giving you the power of a full visual scripting environment while maintaining clean, maintainable backend systems.

***

## Core Functionality

The component tracks dialogue **progress**, manages UI state, supports **branching paths**, and offers rich extensibility with **Blueprint override support** and **manual C++ integration**. Conversations are defined by implementing the `Dialogue()` event in Blueprint or overriding it in C++.

***

### Data Structures

* **`TMap<int32, int32> ActiveProgress`**\
  Tracks the currently selected options for each dialogue "step". Used to determine if a step has been visited and which option was chosen.\
  → Easy to **save/load** for persistence.
* **`FName ActiveBranch` & `TMap<FName, TMap<int32, int32>> BranchProgress`**\
  Optional but powerful. Allows the system to maintain **multiple independent conversation threads** (e.g., for multi-topic conversations).\
  Each branch is stored independently, making it trivial to swap between or reset branches as needed.

***

### Branching Logic

**Dialogue Branches** are fully optional and enable dynamic, multi-path dialogue structures. For example:

```
What would you like to talk about?
- The war    → branch "War"
- The village → branch "Village"
- Never mind → returns to root
```

Each branch remembers progress independently. Players returning to a branch will resume where they left off unless you clear that progress manually. Perfect for **multi-topic NPCs**, **looping dialogue**, or **quest branching**.

Use these nodes to control branch behaviour:

* `Set Dialogue Branch`
* `Get Dialogue Branch`
* `Clear Dialogue Progress`
* `Remove Dialogue Progress`

***

### Blueprint & C++ Integration

The system is designed to be fully usable in either Blueprint or C++, with built-in support for calling parent implementations via `CallParentXXXX` methods. These allow you to call the default `_Implementation` logic from a derived Blueprint or C++ class.

**✅ Blueprint-Callable Nodes:**

| Node Name                    | Description                                                          |
| ---------------------------- | -------------------------------------------------------------------- |
| `Open Conversation`          | Starts a dialogue and pushes widget to the UI stack.                 |
| `CallParentOpenConversation` | Calls the native `_Implementation` of `OpenConversation()`.          |
| `Close Conversation`         | Closes the widget and ends dialogue.                                 |
| `Add Dialogue`               | Adds a new dialogue step (text + options). Increments `ActiveIndex`. |
| `Clear Dialogue Progress`    | Wipes all current dialogue state.                                    |
| `Remove Dialogue Progress`   | Removes the last N steps of dialogue history.                        |
| `Set Dialogue Branch`        | Switch to a different named dialogue path.                           |
| `Get Dialogue Branch`        | Retrieve the current dialogue branch name.                           |
| `Update Selected Option`     | Records a player’s selected option and continues.                    |
| `Progress Dialogue`          | Advances dialogue one step forward, triggering `Dialogue()`.         |

> All nodes are callable from both Blueprint and C++, with consistent naming and behaviour.

***

### Localisation Ready

All dialogue text and options are stored as `FText`, making them automatically compatible with Unreal’s **Localization Dashboard**. No extra steps are needed to enable localisation pipelines for dialogue.

***

### Designer-Friendly Workflow

Dialogue logic is authored inside the `Dialogue()` event, using only standard Blueprint nodes like `Add Dialogue`. This results in a **natural flowchart-like experience**, much like visual novel editors — but with the full power of Unreal behind it.

Because it’s a standard `ActorComponent`, you can:

* Trigger FX, music, scene transitions.
* Play animations.
* Modify lighting or environment.
* Branch based on game state or variables.

No special tools or middleware are required — everything is built with vanilla Unreal Engine systems.

***

## Creating a Dialogue

### Create the Component Class

To create a Dialogue, simply create a new Actor Component derived from DialogueComponentBase. You would then add this component to an Actor such as NPC or an interactable object in your world. When that object is "triggered" such as clicked on by the user or however else you wish to engage this conversation, simply call Open Conversation.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Configure your Dialogue

This will expect you to provide a Common Activatable Widget Stack where it will parent the widget it instantiates.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Set the Widget

You will want to select the Class Defaults and set Widget type (derived from DialogueWidgetBase), this will be instantiated and pushed to the Stack when you call Open Dialogue.

### Implement Event Dialogue

Next implement the event Dialogue.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

This is what is called when the dialogue is opened or advanced; you can think of it like an update loop.

### Add Dialogue Nodes

Now you can add the Add Dialogue nodes to define your "steps"

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

The outputs control the flow through the process

* Option\
  The index of the option selected, which tells you which option the user chose
* Type\
  Pass Through or Updated, if Pass Through, then the system already has a user selection option for this step, so the process should pass through to the next call. if Updated, then we have updated the widget with this text and set of options. You probably want to simply "return", waiting for the widget to trigger the next run when a user selects an option.

### Close Conversation

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

When your ready to end this dialogue, you can call Close Conversation; this will not purge the progression but will remove the widget from the stack.

### Clear Progress

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

This resets the progress on the active branch

### Remove Progress

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

This simply backs the progress up this many steps, no history is kept its simply removing steps from the end of the progress map.

## Working with Branches

If you wish to the branching system, be sure to set the Active Branch if its not already set, its a good idea to use Class Defaults to set your Root Branch name or if you prefer you can set the Active Branch name directly.&#x20;

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Set Branch

To change branches, call Set Branch, providing the name of the new branch you would like to switch to

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

* Dialogue Branch\
  The name of the branch to switch to
* Store Type\
  What to do with the current data if any
  * Clear\
    This will remove the Active branch from memory before setting the next
  * Update\
    This will update the stored values for the Active branch before moving to the next&#x20;

Setting the Branch doesn't automatically progress the dialogue so you can now trigger animations, transitions or whatever else your game calls for. When you are ready to update the widget and progress along call.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
