# Game Client

## Introduction

accessed from within the SteamSettings this houses client specific features and funcitons

## Definition

```csharp
public class SteamSettings : ScriptableObject
{
    public class GameClient;
}
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

### Initalize

```csharp
public void Init();
```

Used internally to intialize the client APIs

### Update All Actions

```csharp
public void UpdateAllActions(InputHandle_t controller);
```

Used to update all known actions for the indicated controller.
