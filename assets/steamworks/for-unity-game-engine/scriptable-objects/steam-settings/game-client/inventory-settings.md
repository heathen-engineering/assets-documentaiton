# Inventory Settings

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

accessed from within the SteamSettings.Client this houses inventory items and provides access to common values such as currency code and change events.

## Definition

```csharp
public class InventorySettings
```

## Fields and Attributes

### LocalCurrencyCode

```csharp
public Currency.Code LocalCurrencyCode => get;
```

Returns the currency code for the local user as reported by Steam.

### LocalCurrencySymbol

```csharp
public string LocalCurrencySymbol => get;
```

Returns the currency symbol (£, $, €, etc.) for the local user's configured currency.

### items

```csharp
public List<ItemDefinition> items;
```

The list of items configured for this app

## Events

### EventChanged

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

###
