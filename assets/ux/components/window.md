---
description: Simple flexable in game windows
---

# Window

## Introduction

{% hint style="info" %}
Part of the [Window System](../features/window-tools.md) of the UX Complete asset
{% endhint %}

The Window component is meant to be applied to a RectTransform game object aka a UI game object and serves as the primary component of the UX Windows system.

## Definition

### Fields and Attributes

| Type    | Name          | Comment                                                                                                                                      |
| ------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Vector2 | minimalSize   | The smallest size the windows Rect will be set to by the Windows system.                                                                     |
| bool    | alwaysOnTop   | If true this window will force its self to the top on each update                                                                            |
| bool    | clampToParent | If true the window will be forced to fall within the bounds of its parent's rect.                                                            |
| bool    | HasFocus      | True if the window has focus. You can set this field to focus this window or if this window is focused you can set it false to remove focus  |
| Vector2 | Position      | Used to get and set the windows position. This will respect the clamp to parent setting                                                      |
| float   | Width         | Used to get and set the width of the window. This will respect the minimal size and clamp to parent setting                                  |
| float   | Height        | Used to get and set the height of the window. This will respect the minimal size and clamp to parent setting                                 |
| Vector2 | Size          | Used to get and set the width and hight at the same time. This will respect the minimal size and clamp to parent setting                     |
| bool    | IsMaximized   | Used to get or set the maximized state of the window                                                                                         |
| bool    | IsMinimized   | Used to get or set the minimized state of the window                                                                                         |

### Events

#### Focused

Available as both a GameEvent and a UnityEvent.

Occurs when the window takes focus

#### Lost Focus

Available as both a GameEvetn and UnityEvent.

Occurs when a query for records complets and contains the results of that query

#### Maximized

Available as both a GameEvent and UnityEvent.

Occurs when the window is maximized

#### Minimized

Available as both a GameEvent and UnityEvent.

Occurs when the window is minimized

#### Restored

Available as both a GameEvent and UnityEvent.

Occurs when the window is restored after a min or max operation

### Methods

```csharp
public void SetTransform(RectTransform transform);
```

```csharp
public void SetTransform(Vector3 position, Vector2 size);
```

Sets the windows position and size to match the target paramiters. If a transform is passed in the windows parentage will not change however it will match the target's position and size.

```csharp
public void Focus();
```

Sets this window as focused.

```csharp
public void Move(Vector2 position);
```

Attempts to move the window to the target position. This respects clamp to parent settings

```csharp
public void Maximize();
```

This will cause the window to fill its parent rect. When doing this the position and size pre-operation is recorded and used by the Restore operation.

```csharp
public void Minimize();
```

This will cause the window to set its size to the minimal allowed by its configuraiton. When doing this the position and size pre-operation is recorded and used by the Restore operation.

```csharp
public void Restore();
```

If currently minimized or maximized this will return the window to its pre operation size. Note that changing the size of a window after it has been minimized or maximized will invalidate this and thus thhe Restore will take no action.

```csharp
public void SnapTo(WindowSnapToLocation location);
```

Snaps the window to a [target location](../enums/window-snap-to-location.md) in its parent e.g. corners and edges.
