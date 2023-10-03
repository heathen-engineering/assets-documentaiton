---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Inventory Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
This tool simply exposes features present in the API and settings to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

The Inventory Manager exposes the Changed event to the inspector which will alert you when the local user's inventory has changed.

This component also exposes commonly use fields from the [SteamSettings.Client.inventory](../scriptable-objects/steam-settings/game-client/inventory-settings.md) settings. This is simply a pass through you do not need to use the Inventory Manager to access these. The purpose of this class is simply to simplify working with the API for user's that are uncomfortable with Scriptable Objects.

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class InventoryManager : MonoBehaviour
```

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
inventroyManager.evtChanged.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    inventroyManager.evtChanged.RemoveListener(HandleEvent);
}
```

### evtTransactionResponce

This is fired whenever Steam client notifies your game of a MTX transaction completing and includes details about that transaction. You can use this along side the [StartPurchase ](inventory-manager.md#startpurchase)feature to know when a transaction starts and ends.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(AppId_t appId, ulong orderId, bool authorized)
{
}
```

Typically you would use the Unity Editor Inspector to attach a method to this event. You can however do it in code as well such as:

```csharp
inventroyManager.evtTransactionResponce.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    inventroyManager.evtTransactionResponce.RemoveListener(HandleEvent);
}
```

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

## Methods

### GetStoreItems

```csharp
public ItemDefinition[] GetStoreItems()
```

Returns the sub-set of items configured for this app that are not hidden, not store hidden and that have a valid price configuraiton. This should be the same set of items visible to Steam's store.
