---
description: Explore the features and services of Heathen's UX
---

# Features

## Feature Comparison

UX is available in two packages, Foundation (free) and Complete (... complete) the following outlines the features of each.

{% hint style="info" %}
Foundation is included with all extension packs and is all that is required to use extensions such as our UI Themes and uGUI Extensions.

In otherwords UX, UI Themes and our uGUI Extensions are standalone and do not require additional purchase.
{% endhint %}

| Features                                        | Foundation | Complete |
| ----------------------------------------------- | ---------- | -------- |
| [System Core](../../system-core/)               | ✔          | ✔        |
| [Cursor System](cursor-tools.md)                | ✔          | ✔        |
| [Command System](command-system.md)             | ✔          | ✔        |
| [Drag and Drop System](drag-and-drop-system.md) |            | ✔        |
| [Interaction Tools](interaction-tools.md)       |            | ✔        |
| [Logging and Feedback Tools](feedback-tools.md) |            | ✔        |
| [Scene Management Tool](scenes-management.md)   |            | ✔        |
| [Screenshot Tool](../api/screenshot.md)         |            | ✔        |
| [Selection System](selection-system.md)         |            | ✔        |
| [Tooltip System](tooltips.md)                   |            | ✔        |
| [Trello Integration](../api/trello.md)          |            | ✔        |
| [Window System](window-tools.md)                |            | ✔        |

### [uGUI Extras](ugui-extras/)

{% hint style="warning" %}
uGUI Extras (and by extension Key Collection) is no longer included in the Complete package.&#x20;



Why?\
Unity now has 3 GUI systems (IMGUI, uGUI and UI Elements) our uGUI Extras are designed to work with Unity's uGUI GUI System, we plan on releasing a UI Elements Extras once the UI Elements System stabilizes. By splitting out the GUI extensions we reduce clutter in frameworks (Foundation and Complete).
{% endhint %}

{% hint style="info" %}
**uGUI Extras is a standalone package**

uGUI Extras contains all the required code to work, you do not need to purchase or install any other packages. UX Foundation and System Core are included with it.
{% endhint %}

uGUI Extras is an extension of UX Foundation that adds uGUI based tools and controls including:

#### [Key Collection](ugui-extras/key-collection.md)

Formerly known as On-Screen Keyboard this tool helps you create and manage collections of buttons simulating virtual keyboards, alliance computer consoles, in game security pads and much more. The control can handle any string output that Unity is capable of rendering including all human languages and any fictional language that can be expressed as simple characters and or ligatures.

#### [Tree View](ugui-extras/tree-view.md)

A simple tool for creating and managing a tree view control where each node in the tree view will be expressed as a uGUI GameObject.

#### Utilties

* Ligature Library\
  Helps you translate character combinations into composite characters useful for complex written languages such as Korean and Japanese as we as common marks such as converting (c) to ©
* Scroll Rect Helper\
  Helps you navigate a scroll view from code, move the scroll view page by page, scroll to a specific item in the view and much more
* Ray Catcher\
  A simple component that handles Canvas Ray Casts without the need of drawing an image or other graphical component.

### UI Themes&#x20;

UI themes are graphics assets and cursors to help you jump start your next project. Each package is themed for a given style and includes all source content as well as UX Foundation with ready to use Cursor States defined for you.
