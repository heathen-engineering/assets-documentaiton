---
description: >-
  Simple, roust flexable tooltips capable of so much more than simply showing
  and hiding panels.
---

# Tooltip System

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The UX Tooltip tools are a simple and flexible approach to driving tooltips in your game. In the simplest form the tool can be thought of as a simple trigger that responds to mouse over event and provides basic feedback to use as a developer, e.g. an event you can listen on an the ability to control delays and similar.

By combining this simple concept with existing tools you can create any sort of tooltip your game may require. From simple popup messages (classic tooltips) to interactive tips with cascading tips contained with in.

## Features

### Triggers

![](<../../../../.gitbook/assets/image (110).png>)

Triggers are available in 3 types but they all serve the same function. They determine when tooltip events should be raised e.g. when should a tip be activated and when should it cancel. They also express the activation state.

{% hint style="info" %}
Notice the ellipsis button to the left of each fields value. These are all [Scriptable Variables](../../../system-core/scriptable-variables.md) and can be set once in your project and shared everywhere or set per game object.

To learn more read up on [System Core's Scriptable Variables](../../../system-core/scriptable-variables.md)
{% endhint %}

#### Game Object Trigger

This is the simplest approach and simply toggles a GameObject's SetActive method e.g. turns a GameObject on or off based on the trigger state.

#### Game Event Trigger

This trigger invokes [Game Events](../../../system-core/game-events.md) when trigger states are changed

#### Unity Event Trigger

This trigger invoked Unity Events when the trigger states are changed

### Window Controller

This component can be used to persist a tooltip open while the user is interacting with it, regardless of the trigger state. Its a simple helper to the system that opens up a number of possibilities including composite tooltips.

{% hint style="info" %}
A composite tooltip is the idea that a tooltip is a window of its own that may have information within it that has additional tooltips.

An example of this can be seen in the demo scene provided with the asset.
{% endhint %}

#### Trigger Invoked

This is a method on the Window Controller that should be called when the window should open. e.g. it should be called by the Tooltip trigger's Invoked event.

#### Trigger Cancelled

This is a method on the Window Controller that should be called when the window's host trigger has cancelled. It will not close the window if the user's pointer is over the window, but does notify the window that the trigger has now entered the cancelled state so should close when the user is no longer interacting with it.

## Configuration

![](<../../../../.gitbook/assets/image (110).png>)

Regardless of the trigger type you choose the core configuration values are as follows

### Trigger Delay

This indicates how many seconds the pointer should be over the trigger before the trigger is activated. When this time has been meet the trigger will be activated invoking any relevant events and setting the `IsActive` field to true.

### Use Cancel Timer

If true then the `Cancel Delay` time will be used to calculate the cancelling of the tooltip. That is when the time in seconds specified in the `Cancel Delay` field has past after the tip has been activated then the cancel events will be invoked and the `IsActive` field will be set to false.

{% hint style="info" %}
In the example above the trigger delay is 2 seconds

The Cancel delay is 5 seconds and the Use Cancel Timer is true

The result is that the tip will be shown when the user has hovered over the trigger for 2 seconds. It will remain open for up to 5 seconds as long as the user hovers over the trigger. It will close anytime the user moves off the trigger.
{% endhint %}

### Invoked and Cancelled Events

{% hint style="warning" %}
Not applicable to the **Tooltip Game Object Trigger**
{% endhint %}

The invoked event will be invoked when the tip is activated. For the **Tooltip Game Event Trigger** this is a [System Core Game Event](../../../system-core/game-events.md) where the **Tooltip Unity Event Trigger** uses standard Unity Events.

{% hint style="info" %}
If your using the Window Controller feature you should use either the Tooltip Game Event Trigger or the Tooltip Unity Event Trigger and you should set the events to invoke the Window Controller's Trigger Invoked and Trigger Cancelled methods
{% endhint %}

## Examples

The tooltip system can in nearly all cases be used with zero code. The following examples describe how to configure various tool tip types in the Unity Editor.

{% hint style="info" %}
In all cases the tooltip system is handling when to invoke or cancel a tip. The content of the tooltip its self is completely up to you as a developer. Unity provides an array of tools capable of handling anything from 3D content to web based content to simple text. The UX Tooltip system is simply causing an action on the "Invoke" aka "Activation" of the time and the "Cancelling" aka "Closing" of the tip.
{% endhint %}

### Simple On/Off Tip

This sort of tip is what you probably expect from most software and web sites and simply shows a popup message when you have moused over something that has more information. To do so you simply need to add a **Tooltip GameObject Trigger** to the object you want the user to mouse over in order to open the tool tip.

![](<../../../../.gitbook/assets/image (111) (1).png>)

Once added you can configure the tip as you would any other and set the "**Target**".

The target tip is simply the GameObject you wish to have activate on trigger activate and deactivate on trigger cancel.

### Invoked Tip

{% hint style="info" %}
Invoked Tips refers to tips driven by an event system and can be done with either or [Tooltip Game Event Trigger](tooltips.md#game-event-trigger) or [Tooltip Unity Event Trigger](tooltips.md#unity-event-trigger)
{% endhint %}

Very often your tips content is rich and needs to perform some run time processing. You could handle this in the "Awake" or "OnEnable" of a custom script such that when the **Tooltip GameObject Trigger** turned the object on your logic ran, and this will work fine but can create several frames where the GameObject is visible but before your process has completed. You may also want to perform calculations to determine what should be turned on if anything and again this works best with an event system as opposed to driving off Unity's OnEnable or similar.

![](<../../../../.gitbook/assets/image (112).png>)

To accomplish this you only need create a function that you wish to have called by the Invoke and another for the Cancel. Using the Tooltip Game Event Trigger or the Tooltip Unity Event Trigger you can connect your invoke and cancel events to the tooltip trigger. You can see a demonstration of this in the demo scene.

### Composit Tip

The idea with a composite tip is a tip window that can be interacted with and may have additional tooltip triggers within its content. A demonstration of this concept can be seen in the demo scene. The set up starts with an invoked tip as described above which will invoke the **TriggerInvoked** method of **TooltipWindowController** on invoked and the **TriggerCanceled** method on canceled just as is show in the above image.

The **TooltipWindowController** would be attached to the root of your 1st level tip. The 1st level tip is the one that is opened initially and may contain child tips attached to its content. The **TooltipWindowController** will keep the window open as long as the user's pointer is hovering over it or any of its children.

{% hint style="info" %}
You can add TooltipWindowController's to the child tips of a composite tip.&#x20;

The tips are not aware of nor do they need to be aware of each other. Unity's IPointerEntere and IPointerExit handler's can handle nested object and will drive the invoke and cancel events accordingly
{% endhint %}

## Use Cases

### Comparison Tips

A common use case for tooltips in most RPGs are comparison tips, that is a tooltip opens showing the details of an item your currently moused over. The display for this may show different text depending on how this item compares to what you currently have equipped. Some games may open an additional tip beside the main tip expressing the values of the compared item.

To accomplish this we recommend using an [Invoked Tip](tooltips.md#invoked-tip) and creating a simple "comparison behavior" to attach to your tip window. Your comparison behavior would have a TriggerInvoked and TriggerCanceled method defined for the Tooltip Trigger to call and these methods would handle the desired process which might look like the following.

1. Determine the information to be shown for the moused over item
2. Determine if we should compare with another item and if so what that other item is
3. If we are comparing items then determine the item we are comparing to
4. Update the UI elements for the tip window according to our needs
5. Finally once the tips are ready we enable the game object at the root of the tip window to show it

### Tutorial Tips

Tutorial Tips are a great way to remind your player of useful information and its customary to give the user a per-tip way of "Don't Show Again" so they can disable a specific tip saving screen clutter. Tutorial tips may also want to run additional logic, such as pause the game on first show and open a more detailed tutorial visual but don't do this on subsequent shows.

To accomplish this we use an approach similar to Comparison Tips in that we would create a custom script to handle the logic specific to our game and then connect that to an [Invoked Tip](tooltips.md#invoked-tip) trigger. Follows are the processing steps your invoke method would likely perform.

1. Determine if the tip should be shown, e.g. has the user previously clicked "Do Not Show" for this or all tips
2. If we should show determine if this is our first showing, if so pause the game and show the detailed tutorial for this section
3. If its not the first show then show the simple tip, this tip might have a toggle on it that the user can flip to prevent this tip from showing again.&#x20;

{% hint style="info" %}
### Scaled Time

The tooltip trigger timers work on unscaled time so will not be adversely impacted by pausing the game in the typical way of setting the time scale to 0.
{% endhint %}

{% hint style="info" %}
### Custom Window Controllers

Your custom script may benefit from the features of **TooltipWindowController**. You could either devise your custom script from it or copy the code and modify it for your own custom window controller.&#x20;

We provide full source so you can learn from and modify our systems to suit your needs.

Remember its better to create a new object based on our code, either by deriving or copy and paste than it is to modify our scripts. This way you can still update as we release patches without breaking your customization.
{% endhint %}

### Gesture UI

Tooltip Triggers can be used for more than informational messages. They are ultimately triggers that respond to mouse enter/exit conditions similar to a button's click even and so can be used like any other user interface action.&#x20;

This would simply be to use the [Invoke Triggers](tooltips.md#trigger-invoked) treating the Invoked and Canceled how you might a Button's click event.
