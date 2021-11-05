# Key Hold

{% hint style="warning" %}
This is for use with Unity's legacy Input System.



You can use Action Hold if your using the new Input System
{% endhint %}

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../features/interaction-tools.md) of the UX Complete asset
{% endhint %}

Ever play a game that asked you to push an hold a button for some period of time to activate the action?

The Key Hold event componenets do just that and are designed to work with Unity's "legacy Input System"

This componenet is available in two flavors

### KeyHoldGameEvent

For use with Heathen Game Events

### KeyHoldUnityEvent

For use with standard Unity Events

## Definition

### Fields and Attributes

| Type       | Name            | Notes                                      |
| ---------- | --------------- | ------------------------------------------ |
| KeyCode\[] | keys            | The keys to monitor, all keys must be held |
| float      | holdTime        | How long the action should be held         |
| bool       | useUnscaledTime | Should time scale be considered            |

### Events

#### Start

Occurs when the action is first started to be held

#### Cancel

Occurs when the action is released before a complete

#### Complete

Occurs when the action is fully held for its duration

#### Progressed

Updated per frame noting the total progress
