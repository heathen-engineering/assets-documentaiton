---
cover: ../../../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Game Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

accessed from within the SteamSettings this houses client specific features and functions

## Definition

```csharp
public class SteamSettings : ScriptableObject
{
    public class GameClient;
}
```

A static accessor is available that will access the active client object

```csharp
SteamSettings.Client
```

## Fields and Attributes

{% hint style="info" %}
Static access fields can also be accessed by reference e.g.

```csharp
GameClient.Inventory
```

is the same as

```csharp
SteamSettings.Client.inventory
```

is the same as

```csharp
mySettings.client.inventory
```
{% endhint %}

<table><thead><tr><th width="210.30334048495172">Type</th><th width="150">Name</th><th width="304.9982296920071">Comments</th></tr></thead><tbody><tr><td>InventorySettings</td><td>Inventory</td><td>Static access to inventory settings</td></tr><tr><td>List&#x3C;<a href="../../input-action-set.md">InputActionSet</a>></td><td>actionSets</td><td>collection of sets mapped from Steam Input</td></tr><tr><td>List&#x3C;<a href="../../input-action-set-layer.md">InputActionSetLayer</a>></td><td>actionSetLayers</td><td>collection of set layers mapped from Steam Input</td></tr><tr><td>List&#x3C;<a href="../../input-action.md">InputAction</a>></td><td>actions</td><td>collection of actions mapped from Steam Input</td></tr></tbody></table>

## Methods

### Initialize

```csharp
public void Init();
```

Used internally to initialize the client APIs

### Update All Actions

```csharp
public void UpdateAllActions(InputHandle_t controller);
```

Used to update all known actions for the indicated controller.
