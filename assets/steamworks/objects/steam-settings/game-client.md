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

### Fields and Attributes

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

| Type              | Name      | Comments                            |
| ----------------- | --------- | ----------------------------------- |
| InventorySettings | Inventory | Static access to inventory settings |

### Methods

```csharp
public void Init();
```

Used internally to intialize the client APIs
