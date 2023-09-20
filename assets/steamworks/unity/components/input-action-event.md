---
description: Listening for input actions
---

# Input Action Event

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

<figure><img src="../../../../.gitbook/assets/image (4) (1) (2).png" alt=""><figcaption></figcaption></figure>

Lets you connect an [InputAction](../scriptable-objects/input-action.md) to a method that takes an [InputActionUpdate ](../../unity-engine/objects/input-action-update.md)value as a parameter in the Unity Editor Inspector similar to the behaviour with a UI Button Click event.

## Events

### Changed

```csharp
public InputactionEvent.ActionDataEvent changed;
```

This event expects a handler that takes an [InputActionUpdate ](../../unity-engine/objects/input-action-update.md)parameter such as.

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
