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
Part of the [Interaction Tools](../features/interaction-tools.md) of the UX Complete asset
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

| Type        | Name            | Notes                              |
| ----------- | --------------- | ---------------------------------- |
| InputAction | action          | The action to monitor              |
| float       | holdTime        | How long the action should be held |
| bool        | useUnscaledTime | Should time scale be considered    |

### Events

#### Start

Occurs when the action is first started to be held

#### Cancel

Occurs when the action is released before a complete

#### Complete

Occurs when the action is fully held for its duration

#### Progressed

Updated per frame noting the total progress

