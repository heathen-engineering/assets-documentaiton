---
description: Create the Steamworks Behaviour on demand
---

# Steamworks Creator

{% hint style="warning" %}
It is strongly recomended that you use a [bootstrap ](../../../company/concepts/bootstrap-scene.md)setup and define the [Steamworks Behaviour](steamworks-behaviour.md) in your [bootstrap](../../../company/concepts/bootstrap-scene.md) scene.&#x20;

The Steamworks Creator is best use in those rare cases where you need to create the [Steamworks Behaviour](steamworks-behaviour.md) on demand or for some other reason must use the older single scene architecture.
{% endhint %}

## Introduction

The Steamworks Creator is a simple script behaviour that allows you to create the Steamworks Behaviour safely, on demand. It does so by checking and insuring there isn't already a Steamworks Behaviour acting on the system and then creating the nessisary objects as required.

{% hint style="info" %}
As noted in the above warning it is strongly recomended that you define the [Steamworks Behaviour](steamworks-behaviour.md) your self, in the editor and use a [bootstrap scene](../../../company/concepts/bootstrap-scene.md) architecture to insure the behaviour is not reloaded.
{% endhint %}

### Steamworks Creator

![](<../../../.gitbook/assets/image (138).png>)

The Steamworks Creator script requries 3 bits of configuration

#### Create On Start

This indicates that the script should create the Steamworks Beahviour on the Unity Start Event if it is missing. When this is set to false the script will not automatically create the behaviour instead you must call the `CreateIfMissing` method your self.

#### Mark As Do Not Destroy

This indicates that the script should mark the created Steamworks Behaviour as Do Not Destroy on Load when it creates it. If this is set false the Steamworks Behaviour game obejct will be created in the active scene and will not be marked as Do Not Destroy On Load.

#### Settings

This is the Steam Settings object that will be applied to the behaviour when it is created. All Steamworks Behaviour objects must reference a valid Steam Settings object.

## Examples

The Steamworks Creator can be used as a static class or as a MonoBehaviour reference

```csharp
public static void SteamworksCreator.CreateIfMissing(SteamSettings settings,
                                                     bool doNotDestroy);
```

The above static method can safely be called at any point in your games execution. It will only create a Steamworks Behaviour object if the Steam API is not already initalized.

You can call this same method from a reference to the Steamworks Creator ... such as in a button click event or other inspector exposed event.

```csharp
public void SteamworksCreator.CreateIfMissing();
```

This funciton will use the SteamSettings and DoNotDestroy value configured on the script behaviour.

In all cases these methods ultimetly call the CreateBehaviour method on the SteamSettings object its self

```csharp
public void SteamSettings.CreateBehaviour(bool doNotDestroy);
```

as such you can call this method your self given your SteamSettings reference such as

```csharp
settings.CreateBehaviour(doNotDestroy);
```

The CreateBehaviour funciton is what performs the tests for initalization so this is a safe call to be made from anywhere in your project.
