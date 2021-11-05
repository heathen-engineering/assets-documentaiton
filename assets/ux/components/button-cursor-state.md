# Button Cursor State

## Introduction

{% hint style="info" %}
Part of the [Cursor System](../features/cursor-tools.md) of the UX Foundation and UX Compelete assets
{% endhint %}

Indicates the cursor state to be applied when the mouse enteres a RectTransfrom and the state to be applied when the mouse is pressed while over the RectTransform.

This is most commonly used with Drag and Drop Items, Buttons, Sliders and anything else the user might click down on and that should show a different mouse pointer when they do.

## Definition

### Fields and Attributes

| Type        | Name            | Notes                                                                   |
| ----------- | --------------- | ----------------------------------------------------------------------- |
| CursorState | stateOnEnter    | The state to apply when the pointer enters the object                   |
| CursorState | stateOnClick    | The state to apply when the object is clicked                           |
| bool        | holdOnMouseDown | Should the state be preserved so long as the mouse button is held down. |

