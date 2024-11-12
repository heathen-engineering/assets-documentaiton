---
description: Simple, flexable window controls in Unity
---

# Windows

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public static class API.Windows
```

Manage RectTransfroms as if they where windows similar to the functionality you would find developing form based applications for Windows and similar operating systems.

### What can it do?

You can add a Window component to any RecTransform to enable the Windows interface to manage that rect as if it where a window. Companion componenets can be used to enable drag to move and resizing funcitonality while the interface its self and features on the Window component can be used to perfrom common window tasks such as minimize, maximize, restore, docking operations, snap to edge and more.

## Events

### Window Focus Changed

```csharp
API.Windows.EventWindowFocusedChanged
```

Invoked when the currently focused window changes. This event will indicate the previously focused and newly focused windows. Note that it is possible that no window was or is now focused thus either can be null.

## Concepts

### Window

A [window ](../components/window.md)is effectivly a RectTransform which has a [Window ](../components/window.md)componenet added to it. This may represent a dialog, menu, panel or similar in your game and is most commonly used as a uGUI based UI element.&#x20;

Though commonly used with uGUI it is not strictly limited to UnityEngine.UI aka uGUI. The Windows API works with RectTransform and the Camera componenets in Unity to manage this rect, what is placed within and how it is rendered is not relivent to the windows interface so you can use anything available in Unity without an issue.

The [Window](../components/window.md) componenet contains much of the same funcitonality you will find in the static API and is defined on a GameObject. It may be simpler in many cases to use the Componenet as opposed to using the API directly.&#x20;

### Focus

A focused window is the window which is currently handling input. This is simulated in Unity by identifying the window where the user last interacted with a UI element or where you have last called "Focus" on the Windows api.

The focused window is automatically moved to the top ... that is, its location in the game object structure will be moved to be the top most child in its current parent and thus Unity will render it on top of all other siblings.

### Clamping

A typical requirement is that a window not be aloud to move or resize outside the bounds of its parent's rect. As such the WIndows API and related components can optionally enforce this restriciton insuring the window cannot be moved or resized through the use of the API to exceed the bounds of the parent rect.

### Tags

This system makes use of the [System Core Tags](../../../assets/system-core/scriptable-tags.md) concept which can be used to search for a given window.

## How To

### Set a window as focused

In most cases you do not need to set this your self. The Window componenet will set windows as focused when the user interacts with them through normal UI controls. In some cases however it can be useful to set a window as focused from code such as to force it to come to the top of the view.

```csharp
API.Windows.Focused = window;
```

{% hint style="info" %}
You can also use the [Window ](../components/window.md)componenet to set that specific window as focused.
{% endhint %}

### Get the focused window

You can read the focused window at any time.

```csharp
var window = API.Windows.Focused;
```

### Set size and position

There are a number of ways to set the size and position of a window.

{% hint style="info" %}
The [Window ](../components/window.md)componenet has similar methods to ones shown here in addition the Move Handle and Border Handle componenets can modify position and size through mouse inputs.
{% endhint %}

```csharp
API.Windows.SetTransform(window, transform);
```

This overload will cause the window to match the RectTransform position and size. Note this does not make the window a child of the indicated transform it simply matches its positon and size. This is most offten used to quickly dock a window to particular place and size.

```csharp
API.Windows.SetTransform(window, postion, size);
```

As the paramiters sugest this will set the size and position of the window in question. Note that position is local space and the pivot point and anchor point considered is always (0.5,0.5) e.g. the middle of the window and middle of the parent.&#x20;

### Min, Max and Restore

Windows can be minimized, maximized and restored to there previous size and position on demand. This works much the same as the minimize, maximize and restore features of the Windows operating system's windows.&#x20;

{% hint style="info" %}
Maximize means to match the size and position of the parent and is the same as calling SetTransform(window, window's parent);
{% endhint %}

{% hint style="info" %}
Minimize means to reduce the windows size to its configured minimal size. If if you wanted to hide the window and show an icon instead you would simply disable the window game object and enable an icon to act as its proxy.
{% endhint %}

### Calculate Clamp

Clamping means to restrict the window to the bounds of its parent, that is limit the windows size and position such that it falls wholly within its parent's rect. You can test for a windows "clamping bounds" by calling

```csharp
var bounds = API.Windows.PositionBounds(window);
```

You can also calculate the valid clamped position of any given position via

```csharp
var validPos = API.Windows.ClampPosition(window, position);
```

### Finding Windows

{% hint style="info" %}
Only registered windows can be found and listed. The Window componenet will automatically register and deregister windows on creation and destroy of the window.
{% endhint %}

You can get a list of all registered windows at any time.

```csharp
var availableWindows = API.Windows.GetAvailableWindows();
```

you can also search for a window based on its scriptable tag or even a Unity tag.

{% hint style="info" %}
It is not recomended to use Unity's tag system.
{% endhint %}

Find the first matching 1 tag

```csharp
var window = API.Windows.FindWindowWithTag(tag);
```

or find all matching 1 tag

```csharp
var windows = API.Windows.FindWindowsWithTag(tag);
```

or fiind the first matching multiple tags

```csharp
var window = API.Windows.FindWindowWithTags(tags);
```

or find all matching multiple tags

```csharp
var windows = API.Windows.FindWindowsWitthTags(tags);
```

or find the first window matching a Unity tag

```csharp
var window = API.Windows.FindWindowWithUnityTag("Dont Do This");
```

or find all windows matching a Unity tag

```csharp
var window = API.Windows.FindWindowsWithUnityTag("Dont Do This");
```

