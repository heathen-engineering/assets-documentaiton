# Cursor State

## Introduction

{% hint style="info" %}
Part of the [Cursor System](../learning/core-concepts/cursor-tools.md) of the UX Foundation and UX Compelete assets
{% endhint %}

A specialized [GameEvent](../../system-core/game-events.md) object which represents the state of a cursor.

## Definition

### Fields and Attributes

| Type                                   | Name        | Notes                                                                      |
| -------------------------------------- | ----------- | -------------------------------------------------------------------------- |
| Vector2                                | hotSpot     | The point in the image to act as the tip or activation point of the cursor |
| [CursorAnimation](cursor-animation.md) | stateOnExit | The animation settings for the cursor                                      |

### Funcitons

#### Set State

Sets the state as active&#x20;

#### Make Default

Makes this the default state
