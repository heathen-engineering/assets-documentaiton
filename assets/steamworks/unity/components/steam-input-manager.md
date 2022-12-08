---
description: Boiler plate start up for Steam Input
---

# Steam Input Manager

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The Steam Input Manager handles the boiler plate aspects of starting and running Steam Input updates. When used you can treat Steam InputAction objects as found in your Steam Settings much like you would an InputAction from Unity's stock system, Rewired or similar systems. For more information about the use of [Steam Input see our How-To and Troubleshooting guides](../guides/input/).

{% hint style="success" %}
If your using Steam Input features then you should add a Steam Input Manager along side your Steamworks Behaviour such that it is never duplicated or destroyed during the game session.
{% endhint %}

## Fields and Attributes

### forceInput

```csharp
public bool forceInput = true;
```

This can only be set in the inspector and simply instructs the tool to force input to your App ID on start up and clear that on destruction. Typically this is only needed when running in the editor.

### AutoUpdate

```csharp
public static bool AutoUpdate { get; set; }
```

Indicates rather or not the system should automatically update all inputs for all controllers every frame. If this is set to false its up to you to call UpdateAll() or alternatively update each controller for each action individually.

### Controllers

```csharp
public InputHandle_t[] Controllers => get;
```

This reads the cashed input handles from Steam. This will default to null and gets refreshed on start of the manager. You can force this to be refreshed by calling RefreshControllers()

## Methods

### UpdateAll

```csharp
public static void UpdateAll()
```

Refreshes all known inputs for all known controllers. This will cause change events to raise and the current InputActionData for every input to update.&#x20;

{% hint style="info" %}
If you have set Auto Update to true then this will be ran for you every frame.
{% endhint %}

### RefreshControllers

```csharp
public static void RefreshControllers()
```

Refreshes the list of known controllers. This is ran for you on start up but can be refreshed at any time such as when controllers are connected or disconnected from the game.
