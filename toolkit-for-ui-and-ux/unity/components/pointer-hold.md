# Pointer Hold

{% hint style="success" %}
Looking for keyboard based hold events?

See

[Action Hold](action-hold.md) for Unity's new Input System

and

[Key Hold](key-hold.md) for Unity's legacy Input System&#x20;
{% endhint %}

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

Ever play a game that asked you to push an hold a button for some period of time to activate the action?

The Pointer Hold event componenets do just that and are designed to work with Unity's "new Input System"

This componenet is available in two flavors

### ActionHoldGameEvent

For use with Heathen Game Events

### ActionHoldUnityEvent

For use with standard Unity Events

## Definition

### Fields and Attributes

<table><thead><tr><th width="184.37677897593124">Type</th><th width="203.52728947555755">Name</th><th width="333.5407480296978">Notes</th></tr></thead><tbody><tr><td>InputAction</td><td>action</td><td>The action to monitor</td></tr><tr><td>float</td><td>holdTime</td><td>How long the action should be held</td></tr><tr><td>bool</td><td>useUnscaledTime</td><td>Should time scale be considered</td></tr></tbody></table>

### Events

#### Start

Occurs when the action is first started to be held

#### Cancel

Occurs when the action is released before a complete

#### Complete

Occurs when the action is fully held for its duration

#### Progressed

Updated per frame noting the total progress

