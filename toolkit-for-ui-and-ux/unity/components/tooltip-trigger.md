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

<table><thead><tr><th width="150">Type</th><th width="150">Name</th><th width="370.2">Notes</th></tr></thead><tbody><tr><td>bool</td><td>isActive</td><td>if false then this trigger will not fire</td></tr><tr><td>float</td><td>triggerDelay</td><td>the time in seconds the trigger will delay activation</td></tr><tr><td>bool</td><td>useCancelTimer</td><td>if true then this trgger will close its self after the indicated time has passed. If false this trigger will only close when it loses activation.</td></tr><tr><td>float</td><td>cancelDelay</td><td>if useCancelTimer is true then this is the number of seconds after the tip is shown before the trigger self cancels.</td></tr></tbody></table>

### Events

#### Invoked

For GameEvent and UnityEvent triggers these are raised when the delay time has passed after the trigger has been activated

#### Canceled

For GameEvent and UnityEvent triggers these are raised when the activation loses focus or if using the cancel timer when the cancel delay time has passed after the tip has been shown.
