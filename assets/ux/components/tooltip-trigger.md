# Tooltip Trigger

## Introduction

{% hint style="info" %}
Part of the [Tooltip System](../learning/core-concepts/tooltips.md) of the UX Complete asset.
{% endhint %}

A tooltip trigger indicates when a tooltip should be shown and then subsaquently hidden. Tooltip Trigger is available in the following forms

### Tooltip Game Event Trigger

Invokes GameEvents when the tip should be activated and cancled respectivly

### Tooltip GameObject Trigger

Toggles a game object's active state when the tip is actiavted and cancled

### Tooltip Unity Event Trigger

Invokes Unity Events when the tip should be activated and cancled respectivly

## Definition

### Fields and Attributes

| Type  | Name           | Notes                                                                                                                                             |
| ----- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| bool  | isActive       | if false then this trigger will not fire                                                                                                          |
| float | triggerDelay   | the time in seconds the trigger will delay activation                                                                                             |
| bool  | useCancelTimer | if true then this trgger will close its self after the indicated time has passed. If false this trigger will only close when it loses activation. |
| float | cancelDelay    | if useCancelTimer is true then this is the number of seconds after the tip is shown before the trigger self cancels.                              |

### Events

#### Invoked

For GameEvent and UnityEvent triggers these are raised when the delay time has passed after the trigger has been activated

#### Canceled

For GameEvent and UnityEvent triggers these are raised when the activation loses focus or if using the cancel timer when the cancel delay time has passed after the tip has been shown.
