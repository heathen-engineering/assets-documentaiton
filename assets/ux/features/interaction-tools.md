---
description: Tools to help your game be more responsive
---

# Interaction Tools

## Introduction

{% hint style="info" %}
Available in UX [Complete](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)
{% endhint %}

Interaction Tools is a collection of simple behaviors that help you deliver a more responsive user experience quickly, easily and with a high degree of quality.

## Features

### Hold Event

These tools help you create hold event actions for your players and they come in a few flavors. A hold event is when your interface asks the player to click on a GUI element or press a specific button for some duration in order to activate the action.

![](<../../../.gitbook/assets/image (113).png>)

All hold events let you specify the hold time and rather or not the system should use unscaled time.

Hold events are a nice alternative to confirmation popups and can be implemented as mouse events, Unity's new Input System action events or as legacy Input Manager's key events. Regardless of which variant you use they will all handle the following events.

| Event      | Use                                                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Started    | Invoked when the user first engages the interface element                                                                                        |
| Canceled   | Invoked if the user canceled the operation before it completes                                                                                   |
| Completed  | Invokes if the user holds the engagement for the specified duration                                                                              |
| Progressed | Invokes every frame that the user is holding the engagement, this will pass a float value between 0 and 1 indicating the progress at that frame. |

Each type of hold has a Game Event and Unity Event variant. That is you can either have the hold invoke Game Events for each phase or Unity Events for each phase.

{% hint style="info" %}
If you wanted the system to raise both Game Events and Unity Events the most efficent method would be to have the Unity Event invoke the Game Events.
{% endhint %}

#### Action Hold

This variant takes an Input Action (Unity's new Input System)&#x20;

#### Key Hold

{% hint style="warning" %}
This variant type can take 1 or more KeyCodes. all KeyCodes provided must be held for the engagement to be registered.
{% endhint %}

This variant takes a collection of KeyCodes (Unity's legacy Input System)

#### Pointer Hold

This variant uses Unity's IPointer Down, Up and Exit handlers so will respond to mouse, touch, and anyhting else that triggers Unity's IPointer handlers.

### Play On audio tools

Play On audio tools are simple components which will play an audio clip on the indicated events. This makes for a very simple system for applying UI audio.

![](<../../../.gitbook/assets/image (114).png>)

Each Play On component takes an Output audio source and a Sound audio clip and can configure the Volume Scale of the clip. The Play On will play the clip through the output source when its engaged. The following variants are available.

#### [Play On Click](../components/play-on-click.md)

This plays when the GameObject is clicked (uses iPointerClickHandler). You can configure rather or not the system should monitor left, right and middle clicks.

#### [Play On Demand](../components/play-on-demand.md)

This plays when its PlayOneShot method is called. This can be used with other tools such as Buttons by attaching the PlayOneShot method to the button's Click event.

#### [Play On Down](../components/play-on-down.md#fields-and-attributes)

This plays when the GameObject is pressed (mouse down), (uses iPointerDownHandler). You can configure rather or not the system should monitor left, right and middle clicks.

#### [Play On Enter](../components/play-on-enter.md)

This plays when the GameObject is entered (uses iPointerEnterHandler).

#### [Play On Exit](../components/play-on-exit.md)

This plays when the GameObject is exited (uses iPointerExitHandler).

#### [Play On Up](../components/play-on-up.md)

This plays when the GameObject is released (mouse up), (uses iPointerUpHandler). You can configure rather or not the system should monitor left, right and middle clicks.

