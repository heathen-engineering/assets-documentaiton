---
description: Tools, systems and frameworks to help you deliver a superior User eXperience!
---

# User eXperience \[UX]

{% hint style="info" %}
The UX articles are a work in progress and being updated frequently. If you have any questions at all please reach out over [Discord](https://discord.gg/6X3xrRc)
{% endhint %}

{% embed url="https://discord.gg/6X3xrRc" %}

## Introduction

Heathen’s UX product enable you to deliver a richer, more robust, and more polished experiences to your customers and does so while saving you significant time in development in testing.&#x20;

{% embed url="https://youtu.be/uZn9HN1vGmw" %}

Heathen’s UX support you and your project with flexible, battle tested tools and systems that are both easy to use and easy to extend and customize. UX is built on top of Heathen’s System Core, comes with full source code, detailed documentation, a large community and of course Heathen’s support and on-going development.

### Key Features

[Drag and Drop](learning/core-concepts/drag-and-drop-system.md)

Create smart drag and drop systems with simple masks and filters code free

[Animated Cursor](learning/core-concepts/cursor-tools.md)

Create context sinsative animated mouse cursors with zero code

[Tooltip System](learning/core-concepts/tooltips.md)

Create tooltips, popups and cascade windows with easy to use triggers

[Window System](learning/core-concepts/window-tools.md)&#x20;

Create UI windows that can be daged, resized, docked and more

[Advanced Log](learning/core-concepts/feedback-tools.md)

Gather detailed data in a serializable formate great for use with tools like Unity's Feedback, Zendesk Unity integration, Trello integraiton and more.

## UX v2 vs V1

Heathen’s UX v2 is the next major update to our User eXperience tools and represents a full rewrite of every system and the addition of many new systems and tools taken from our own internal projects.

### UIX v1

UIX \[User Interface Experience] (aka v1) was Heathen’s first Unity asset (published then as On-Screen Keyboard) and was published in 2014. It has been continuously supported and upgraded through many major Unity updates. As you might imagine the long-term growth of v1 meant many aspects of the system were relics of bygone Unity’s 😉 and in need of a full rewrite to both remove unused legacy concepts and introduce new features that didn’t align with older designs.

### UX v2

UX v2 expands the scope to include all aspects of the user experience, not just interface elements, hence the dropping of the I in the name. We have gone through and fully restructures and rewritten the assets maintaining all the same functionality of previous generations, and added many new features we ourselves have been using in our internal projects.

{% hint style="info" %}
UX v2 conforms to Heathen’s more modular approach to asset development and organization making it easy for you to use just the parts you want and strip out the rest keeping your project lean and efficient.
{% endhint %}

## Feature Comparison

UX is available in two packages, Foundation (free) and Complete (... complete) the following outlines the features of each.

{% hint style="info" %}
Foundation is included with all extension packs and is all that is required to use extensions such as our UI Themes and uGUI Extensions.

In otherwords UX, UI Themes and our uGUI Extensions are standalone and do not require additional purchase.
{% endhint %}

| Features                                                               | Foundation | Complete |
| ---------------------------------------------------------------------- | ---------- | -------- |
| [System Core](../system-core/)                                         | ✔          | ✔        |
| [Cursor System](learning/core-concepts/cursor-tools.md)                | ✔          | ✔        |
| [Command System](learning/core-concepts/command-system.md)             | ✔          | ✔        |
| [Drag and Drop System](learning/core-concepts/drag-and-drop-system.md) |            | ✔        |
| [Interaction Tools](learning/core-concepts/interaction-tools.md)       |            | ✔        |
| [Logging and Feedback Tools](learning/core-concepts/feedback-tools.md) |            | ✔        |
| [Scene Management Tool](learning/core-concepts/scenes-management.md)   |            | ✔        |
| [Screenshot Tool](api/screenshot.md)                                   |            | ✔        |
| [Selection System](learning/core-concepts/selection-system.md)         |            | ✔        |
| [Tooltip System](learning/core-concepts/tooltips.md)                   |            | ✔        |
| [Trello Integration](api/trello.md)                                    |            | ✔        |
| [Window System](learning/core-concepts/window-tools.md)                |            | ✔        |

### [uGUI Extras](learning/ugui-extras/)

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

#### [Key Collection](learning/ugui-extras/key-collection.md)

Formerly known as On-Screen Keyboard this tool helps you create and manage collections of buttons simulating virtual keyboards, alliance computer consoles, in game security pads and much more. The control can handle any string output that Unity is capable of rendering including all human languages and any fictional language that can be expressed as simple characters and or ligatures.

#### [Tree View](learning/ugui-extras/tree-view.md)

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
