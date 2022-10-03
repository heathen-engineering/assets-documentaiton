---
description: >-
  Create smooth, responsive context sensitive and animated cursors for your
  game.
---

# Cursor System

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The cursor system allows for easy code free context sensitive mouse cursors with support for animation.

![](<../../../../.gitbook/assets/image (153) (1) (1) (1) (1).png>)

The Cursor Animator component handles cursor animation, you should only have 1 of these active at any given time.

{% hint style="info" %}
This component benefits from the [bootstrap](../../../../company/concepts/fundamentals/bootstrap-scene.md) concept which you can read more about [here](../../../../company/concepts/fundamentals/bootstrap-scene.md)
{% endhint %}

With an active Cursor System you can effect the state of the pointer by attaching Cursor State components to desired game objects or through code where you want or need a more bespoke solution.

## Cursor State

A cursor state is a scriptable object derived from [GameEvent](../../../system-core/game-events.md)\<bool> which represents a state that the game's pointer can be in.

{% hint style="info" %}
Cursor States are [GameEvents](../../../system-core/game-events.md) of type bool, meaning that when the state is set or removed it is "invoked" raising the game event and indicating its state. As such you can create an event driven system that responds to states being activated or deactivated by simply adding a listener to the state.

```csharp
cursorState.AddListener(HandleThisStateChanged);
```

You can then handle the event as such

```csharp
void HandleThisStateChanged(EventData<bool> param)
{
    //The sender will be the state that was changed
    var state = param.sender as CursorState;
    //The value will be true if activated false if deactivated
    Debug.Log(state.name 
    + (param.value ? " is active" : " is inactive"));
}
```
{% endhint %}

### Hot Spot

A `Vector2` representing the hot spot of the cursor e.g. the "tip" in the case of an arrow or wedge or a pointing finger. This is the finite location of the pointer.

### Animation

A `CursorAnimation` field, this is a custom object which defines the settings of a simple texture animation.

#### Animation.Loop

Indicates rather or not the animation should loop endlessly or if it should animate to the end and hold the last frame

#### Animation.TextureArray

The set of textures to be animated through. Each frame should be its own texture and should have the same hot point as is defined on the Cursor State.

#### Animation.FramesPerSecond

How many frames should be shown in 1 second. This value is used to determine the time per frame dictating the speed of the animation.

## System Configuration

The cursor system works with a concept of "Cursor State", a state defines the icon to be used and the settings for its animation. At run time the state can be changed by triggers such as Mouse Over Cursor State behavior.

### Default State

This default state is the state the system will return to when a component state is no longer true; for example when your pointer exits a Mouse Over Cursor State object it will return to the Default State you defined in the Cursor System.

### Cursor Mode

Defaults to Auto, this indicates what type of cursor the game should use. Software Cursors can be more flexible in terms of what you can do with them, however they also tend to show a lag or latency and so Auto or Hardware is recommended.

## Hold On Mouse Down

Hold on mouse down is a feature of the Set State function of Cursor System. When a state is being applied, it can optionally be applied as "**Hold On Mouse Down**". This indicates to the system that if the left mouse button is pressed while the state is active that the state should persist for as long as the left mouse button is held.

Hold On Mouse Down is most often used with drag features such as drag and drop UI elements, drag to resize handles on [windows ](window-tools.md)and drag to move handles on windows. This insures that the cursor doesn't switch to default as the mouse is moved around and gives a more natural feel to the user.

You can configure [Mouse Over Cursor State](cursor-tools.md#mouse-over-cursor-state) and [Button Cursor State](cursor-tools.md#button-cursor-state) to set the Hold On Mouse Down value when they are activated. The Hold On Mouse Down value can also be set from code when setting a state.

```csharp
SetState(CursorState state, bool setOnDown, bool holdOnDown);
```

{% hint style="info" %}
Set On Down the second parameter when set true will cause any current holding state to be overridden with this state.

That is if the system is currently holding a state active due to Hold On Mouse Down, then by passing true into Set On Down the system will override that state with the new state. This is used by Button Cursor State to apply the State On Click value.
{% endhint %}

## Mouse Over Cursor State

![](<../../../../.gitbook/assets/image (99).png>)

This simple component can be added game objects and will cause the state of the cursor to change when the mouse enters the object. Optionally the state can be set to hold on mouse down, which can be useful of hand grab icons such as might be used for a drag to scroll UI element.

## Button Cursor State

![](<../../../../.gitbook/assets/image (100).png>)

The button cursor state handles two (2) possible state changes, one for mouse enter similar to the Mousse Over Cursor State and one for On Click. This allows the component to show a 2nd cursor state while the mouse is held down such as highlighted pointer or tapping finger.

## Change Cursor Default State

![](<../../../../.gitbook/assets/image (101) (1).png>)

The change cursor default state will change the registered default state on enter and exit.

## Examples

In most cases the desired effects can be handled code free, however the system is also designed with programmers in mind and has an easy to use interface. Most of the examples below will require a reference to a desired CursorState. Generally this reference would be set at development time much like you would any reference in Unity.

```csharp
public class SomeBehaviour : MonoBehaviour
{
    public CursorState cursorState;
}
```

You can then simply drag the desired state into the "Cursor State" field in the Unity Inspector.

### Set Active

The most common way to set state would be to use the [Mouse Over Cursor State](cursor-tools.md#mouse-over-cursor-state) or [Button Cursor State](cursor-tools.md#button-cursor-state) components, however you can also set the state from code.

#### From the state

```csharp
//The same as calling SetActive(this, false, false);
cursorState.Active = true;
```

or

```csharp
cursorState.SetActive(setOnHold, holdOnDown);
```

#### From Cursor System

```csharp
CursorSystem.SetActive(cursorState, setOnHold, holdOnDown);
```

### Get Active

#### From the state

```csharp
var isActive = cursorState.Active;
```

#### From Cursor System

```csharp
var activeState = CursorSystem.CurrentState;
```

### Cursor State Event

The Cursor State object is derived from [GameEvent\<bool>](../../../system-core/game-events.md) and so you can define an event driven structure with changes in pointer state.&#x20;

```csharp
cursorState.AddListener(HandlerFunction);
```

The handler should take a single parameter of type EventData\<bool>

```csharp
private void HandlerFunction(EventData<bool> data)
{
    //The sender is the CursorState
    var cursorState = data.sender as CursorState;
    
    //The value indicates rather it was activated or deactivated
    if(data.value)
        Debug.Log(cursorStae.name " was activated");
    else
        Debug.Log(cursorStae.name " was deactivated");
}
```
