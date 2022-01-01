# Inventory Manager

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

{% hint style="info" %}
This tool simply exposes features present in the API and settings to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

## Introduction

The Inventory Manager exposes the evt Changed event to the inspector which will allert you when the local user's inventory has changed.

This componenet also exposes commonly use fields from the [SteamSettings.Client.inventory](../objects/steam-settings/game-client/inventory-settings.md) settings. This is simply a pass through you do not need to use the Inventory Manager to access these. The purpose of this class is simply to simplify working with the API for user's that are uncomfrotable with Scriptable Objects.

## Fields and Attributes

### CurrencyCode

```csharp
public Currency.Code CurrencyCode => get;
```

Returns the currency code as read from Steam

### CurrencySymbol

```csharp
public string CurrencySymbol => get;
```

Returns the string symbol (£, $, €, etc.) related to the currency code as read from Steam.

### Items

```csharp
public string List<ItemDefinition> Items => get;
```

Returns the list of items configured for this app

## Events

### evtChanged

Triggered whenever the local user's inventory is updated from Steam.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(InventoryChangeRecord arg0)
{
}
```

Then you would register the event such as:

```csharp
SteamSettings.Client.inventory.EventChanged.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    SteamSettings.Client.inventory.EventChanged.RemoveListener(HandleEvent);
}
```

## Methods

### GetStoreItems

```csharp
public ItemDefinition[] GetStoreItems()
```

Returns the sub-set of items configured for this app that are not hidden, not store hidden and that have a valid price configuraiton. This should be the same set of items visible to Steam's store.
