---
description: Easy to use and efficent animated and context sinsative pointers
---

# Cursors

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public static class API.Cursors
```

The cursors interface manages the default and current cursor state for your application.&#x20;

### What can it do?

* Animated pointers / cursors
* Context sinsative pointers
* Manage mouse features such as lock, visible, render mode and more
* Create and control animated pointers as Scriptable Objects
* Listen to cursor states as Game Events being notified be each state when its activated or deactived

## Events

Each cursor state is a [Game Event ](../../../assets/system-core/game-events.md)as such each state can be listened to and will invoke when it is enabled or disabled e.g. when the state becomes active or is replaced by another state.

## Concepts

### [Cursor State](../objects/cursor-state.md)

A cursor state is a simple Scriptable Object which difines the details of a particular pointer. You can specify the image or an array of images to use, an animation speed if relivent as well as the hot point of the pointer.

Cursor States are [Game Events](../../../assets/system-core/game-events.md) of type bool which invoke when activated or deactivated.&#x20;

#### Members

```csharp
public Vector2 hotSpot;
```

The hot spot indicates the pixel in the image used as the origin or click point of the pointer

```csharp
public CursorAnimation animation;
```

The animation defines the array of images to be used for the animation as well as the frames per second and rather or not the animation should loop or stop at the end. Cursors that do not animate would simply have a single image in the array.

```csharp
public bool Active { get; set; }
```

Active can be used to get or set the state on the pointer. If you assinge true to the Active field then this state will be made active on the mouse pointer, if you assigne false then it will be removed if present and the default state assigned.

{% hint style="warning" %}
Setting a state's Active field to false that is not currently active has no effect. The current cursor state will only be set to default if you assigne the currently active state to Active = false.
{% endhint %}

```csharp
public void SetState(bool setOnHold, bool holdOnDown);
```

Sets the active cursor to this cursor and optionally overrides the holding state. See the API.Cursors.SetState section for details

```csharp
public void MakeDefault();
```

This simply makes this state the default state, the default state is the state the cursor is set to when all states are cleared or deactivated.

### Default State

The default state is simply a Cursor State that has been designated as the state the system should return to when all other states are cleared. You can set the Default State through a number of different mechinisms.

```csharp
//Assuming
CursorState myState;
// ... then
myState.MakeDefault();
```

```csharp
//Assuming
CursorState myState;
// ... then
API.Cursors.DefaultState = myState;
```

Or you can use the Cursor Animator or Change Cursor Default State components to set the default currsor state.

### [Cursor Animation](../objects/cursor-animation.md)

This is the data type of the CursorState.animation attribute and defines the nature of the animation to be used for a given cursor state.

```csharp
public bool loop = false;
```

Should this animation loop, if true the animation will return to frame 1 when it reaches the end, otherwise it will hold on the last frame.

```csharp
public Texture2D[] textureArray;
```

The array of "frames" for the animation, the system will cycle over these at the rate indicated by the frames per second attribute.

```csharp
public float framesPerSecond = 30;
```

The aproximate number of frames to show per second. Note this is limited by the performance of the game e.g. if your game is running at 20 frames per second then the animation will run at 20 frames per second.&#x20;

{% hint style="info" %}
In general this should be set as low as possible to yield a quality result. You should strive to keep this value notably lower than the game's running FPS otherwise a visible stutter in the animation will be visible as it cannot run faster than the games update loop.
{% endhint %}

## How To

### Change Render Mode

You can change the rendering mode of the cursor at any time. Remode options are hardware and software. In most every instance its preferable to use hardware as your rendering mode.

```csharp
API.Cursors.RenderMode = desiredMode;
```

### Change Visibility

You can set the visibility of the cursor at any time. If set to true the cursor will be rendered else it will not. Note that the cursor still exists and still funcitons it is simply not rendered if set to false.

```csharp
API.Cursors.Visible = true;
```

### Locking the pointer

You can optionally lock the pointer to the screen or to the centre of the screen this is commonly done in first person shooters in particular when you have made the pointer invisible.

```csharp
API.Cursors.LockMode = desiredMode;
```

### Set the Default Cursor

You can set the default cursor at any time.

{% hint style="info" %}
You can also use the Cursor Animator and Change Default Cursor State componenets to set the default cursor to a particular state.
{% endhint %}

```csharp
API.Cursors.DefaultCursor = desiredCursorState;
```

### Set state to Default

You can clear the current sate e.g. set the default state active at any time.

```csharp
API.Cursors.SetDefault();
```

### Set Current State

You can set the current cursor state at any time.

```csharp
API.Cursors.CurrentState = desiredCursorState;
```

or

```csharp
API.Cursors.SetState(state, setOnHold = false, holdOnDown = false);
```

{% hint style="warning" %}
When `holdOnDown` is true then the cursor state will persist as long as the left mouse button is held down. This is commonly used for button click cursors such that the cursor remains in that state even if the pointer is dragged off the button. This may also be useful for game context cursors such as an attack cursor
{% endhint %}

{% hint style="warning" %}
When setOnHold is true then the state will be applied even if the system is currently holding an existing state ... that is if true then this will force this state to be applied even if the current state displaying is a "holdOnDown" state that is being preserved while the mouse button is down. This can be useful for drag and drop sitautions.
{% endhint %}

{% hint style="info" %}
You can also set the state of the currsor using the Mouse Over Cursor State component. This commonent adjusts the cursor state based on mouse enter and exit events.
{% endhint %}
