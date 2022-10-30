---
description: Listening for input actions
---

# Input Action Event

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Lets you connect an [InputAction](../scriptable-objects/input-action.md) to a method that takes an [InputActionUpdate ](../../objects/input-action-update.md)value as a parameter in the Unity Editor Inspector similar to the behaviour with a UI Button Click event.

## Events

### Changed

```csharp
public InputactionEvent.ActionDataEvent changed;
```

This event expects a handler that takes an [InputActionUpdate ](../../objects/input-action-update.md)parameter such as.

```csharp
public void HandleActionEvent(InputActionUpdate data)
{
    //Do Work
    if(data.State)
        ;//This action happened
}
```

### Fields and Attributes

### Action

```csharp
public InputAction action;
```

A reference to the action to listen on. This action will invoke the Changed event when its data has changed as a result of update from the Steam Input system.
