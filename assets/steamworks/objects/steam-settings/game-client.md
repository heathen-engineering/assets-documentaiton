# Game Client

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
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

| Type                                                      | Name            | Comments                                         |
| --------------------------------------------------------- | --------------- | ------------------------------------------------ |
| InventorySettings                                         | Inventory       | Static access to inventory settings              |
| List<[InputActionSet](../input-action-set.md)>            | actionSets      | collection of sets mapped from Steam Input       |
| List<[InputActionSetLayer](../input-action-set-layer.md)> | actionSetLayers | collection of set layers mapped from Steam Input |
| List<[InputAction](../input-action.md)>                   | actions         | collection of actions mapped from Steam Input    |

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
