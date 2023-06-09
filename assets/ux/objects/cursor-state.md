# Cursor State

## Introduction

{% hint style="info" %}
Part of the [Cursor System](../learning/core-concepts/cursor-tools.md) of the UX Foundation and UX Compelete assets
{% endhint %}

A specialized [GameEvent](../../system-core/game-events.md) object which represents the state of a cursor.

## Definition

### Fields and Attributes

<table><thead><tr><th width="186.68968107781367">Type</th><th width="182.41271262309755">Name</th><th width="370.2">Notes</th></tr></thead><tbody><tr><td>Vector2</td><td>hotSpot</td><td>The point in the image to act as the tip or activation point of the cursor</td></tr><tr><td><a href="cursor-animation.md">CursorAnimation</a></td><td>stateOnExit</td><td>The animation settings for the cursor</td></tr></tbody></table>

### Funcitons

#### Set State

Sets the state as active&#x20;

#### Make Default

Makes this the default state
