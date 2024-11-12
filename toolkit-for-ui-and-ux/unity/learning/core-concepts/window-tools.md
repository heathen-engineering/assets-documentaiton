---
description: Easily manage in game windows, panels and dialogs.
---

# Window System

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

The Window system makes it easy to define drag-able, re-sizable and dock-able windows in your game. The simple system can be attached to any Rect Transform and supports all canvas modes and all anchoring types. Window groups can be defined easily by simply parenting them in there own Rect Transforms where windows focus (move to top) and clamp (remain in frame) according to there parent.

{% hint style="info" %}
Check out the following articles for more details on specific components

[Window](../../components/window.md)

[Move Handle](window-tools.md#move-handles)

[Border Handle](window-tools.md#border-handles)
{% endhint %}

![](<../../../../.gitbook/assets/image (152) (1) (1) (1).png>)

With this system, you have complete control of your window's features including resize and move handles. You can choose to add a move handle, allowing the window to be dragged around the parent, rather or not it clamps to the parent and rather or not it remains always on top of other windows.

![](<../../../../.gitbook/assets/image (80).png>)

## Searchable Windows

The API.Windows interface makes it easy to search for and manage all available windows and identify the currently focused window. Windows use the Selectable Tag system meaning you can tag your windows with multiple tags and search for windows with matching tags.

For more information please review the [API.Windows interface article](../../api/windows.md).

## Configuration

### Move Handles

![](<../../../../.gitbook/assets/image (85).png>)

Intended to be added to a child object of your window the RecTransform this is added to will be the clickable area that when clicked allows the user to drag the window.

{% hint style="info" %}
Works great with the [Cursor Tools](cursor-tools.md) Button Cursor State
{% endhint %}

### Border Handles

![](<../../../../.gitbook/assets/image (86).png>)

Similar to the Move Handle, the Border Handle is intended to be added to a child object of your window, the RectTransform of which will be the clickable area that when click allows the user to drag to resize the window. Border Handles need to be told what part of the border they are on as this effects the drag to resize behaviour.

#### Handle Types

* Top\
  Drag increases the height of the window from its top edge
* Bottom\
  Drag increases the height of the window from its bottom edge
* Left\
  Drag increases the width of the window from its left edge
* Right\
  Drag increases the window of the window from its right edge
* Upper Left\
  Drag increases the height and width of the window from its upper left corner
* Upper Right\
  Drag increases the height and width of the window from its upper right corner
* Lower Left\
  Drag increases the height and width of the window from its lower left corner
* Lower Right\
  Drag increases the height and width of the window from its lower right corner

## Examples

### Get the focused window

```csharp
public static Window focused;
```

You can get the Window object that is currently focused from the static focused attribute.

```csharp
var focusedWindow = Window.focused;
```

### Focus a Window

This assumes the window you wish to give focus to is named `targetWindow`

{% hint style="info" %}
This set the target window as the Window.focused and moves the window to be on top of **non-Always On Top** windows.
{% endhint %}

```csharp
targetWindow.Focus();
```

### Set or Get Position

This example assumes the window to be moved is named `targetWindow` and that you wish to move it to a location defined as `position`

```csharp
//Get the position
position = targetWindow.Position;

//Set the position
targeWindow.Position = position;
```

{% hint style="info" %}
This respects the "anchor" you set in Unity's Rect Transform. For example if you want the window to move relative to its upper left corner then you should set the anchor position of its Rect Transform to the upper left corner.
{% endhint %}

### Set or Get Width

This example assumes the window to be sized is named `targetWindow` and that you wish to set its size to a value defined as `width`

```csharp
//Get the width
width = targetWindow.Width;

//Set the width
targetWindow.Width = width;
```

{% hint style="info" %}
This respects the "anchor" you set in Unity's Rect Transform. For example if you want the window to move relative to its upper left corner then you should set the anchor position of its Rect Transform to the upper left corner.
{% endhint %}

### Set or Get Height

This example assumes the window to be sized is named `targetWindow` and that you wish to set its size to a value defined as `height`

```csharp
//Get the height
height = targetWindow.Height;

//Set the height
targetWindow.Height = height;
```

{% hint style="info" %}
This respects the "anchor" you set in Unity's Rect Transform. For example if you want the window to move relative to its upper left corner then you should set the anchor position of its Rect Transform to the upper left corner.
{% endhint %}

### Transform the window

This will set the windows position and size at the same time.

```csharp
targetWindow.SetTransform(size, position);
```

### Dock Window

This will snap the window to the position and size of the input RectTransform.

{% hint style="warning" %}
Scale is not accounted for in this operation. Its advised that you dock to transforms that in the same canvas or otherwise are at the same global scale as the window.
{% endhint %}

```csharp
targetWindow.DockTo(targetRect);
```
