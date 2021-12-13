# Scenes Manager

## Introduction

{% hint style="info" %}
Part of the [Scenes Tools](../learning/core-concepts/scenes-management.md) of the UX Complete asset
{% endhint %}

This componenet simply exposes events and features present on the [API.Scenes](../api/scenes.md) interface to the Unity Inspector for ease of use. This componenet can be used to drive progress bars and other elements that need to respond to scene processing events.

You can use as many Scenes Manager componenets as you like in as many scenes as you like, all funcitonality and data is actually stored in the API.Scenes interface and is not impacted by the existance or lack of existances of a Scenes Manager object.

## Definition

### Events

All events are available as Unity Events and Heathen [Game Events](../../system-core/game-events.md)

#### Started

Occurs when a scenes operation starts, this may be a load, unload or both

#### Updated

Occurs each frame a scene operation updates

#### Completed

Occurs when a scenes operation completes

### Funcitons

All funcitons listed here are available on this componenet but are actually executed on the [API.Scenes](../api/scenes.md) interface, these are listed on this object for ease of use with Unity Inspector and tools such as Bolt.

#### [Transition](../api/scenes.md#transition-between-scenes)

#### [Load](../api/scenes.md#additive-load-unload)

#### [Unload](../api/scenes.md#additive-load-unload)

#### [Set Active](../api/scenes.md#set-scene-active)
