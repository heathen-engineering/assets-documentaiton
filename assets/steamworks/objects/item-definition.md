---
description: Defines a Steam Inventory Item
---

# Item Definition

## Introduction

The Item Definition provides access to core features of Steam Inventory Items. This object is represented as a Scriptable Object within you Steam Settings object and has features of conveance proivdeing short cuts to core funcitons of the Steam Inventory interface.

## What can it do?

The Item Definition provides easy access to common features of the Steam Inventroy interface. in particular most of the item specific features are accessable directly through the Item Definition object.

## How To

### Add Promo Item

Short cut to the Add Promo Item of the API.Inventory interface.&#x20;

```
item.AddPromoItem(callback);
```

### Consume

You can use the Item Definition to consume 1 or more instances of the item with simple method calls.

#### Consume a single instance

This is the simplest and most common approch, it assumes you are consuming a single instance of the item.

```
item.Consume(callback);
```

#### Consume multiple

When consuming multiple instnaces we need to first get a set of orders.&#x20;

{% hint style="info" %}
Steam Inventory Items may have zero (0) or many item details which will consist of zero (0) or many instances each. its simplest to think of an Item Detail as a stack of that type of item. Each stack may have 0 or many items of that type in it. When consuming we need to indicate the stack to consume from and how many to consume from that stack. That is what the GetConsumeOrders method does, it provides a refernce to which stacks should consume how many to result in the total you indicated.

Example:

* instance A = 4 quantity
* instance B = 0 quantity
* instance C = 2 quantity
* instance D = 3 quantity

In this case the user has a total of 9 of this item spread across 4 insances. If you requested to consume 5 of this item you would get 2 orders back.&#x20;

1. Order 1 would contain 4 from instance A
2. Order 2 would contain 1 from instance C

Once you had the orders its up to you to call the Consume method on the order.
{% endhint %}

```csharp
var orders = item.GetConsumeOrders(quantity);
foreach(var order in orders)
{
    item.Consume(order, callback);
}
```

### Exchange

{% hint style="warning" %}
To exchange some items for another item, the item you wish to exchange for must define the recipie of items in its Item Definition as upoloaded to Steam's portal.



The item recipie is how this is able to run client side, since the item definition defines what exchanges are valid, and the Steam backend controls what items the player owns then Steam can assuradly confirm that a recipie is valid.
{% endhint %}

An exchange, exchanges some set of items for some other item. Its most simple to think of this as crafting, you provide some set of ingrediants and the result is some single item. When you call Exchange on an item you provide a set of items and if the process is succesfult you will recieve evidence of a new instnace of this item in the player's inventory.

To start the proces you must first identify the specifc item instnaces to be consumed. How you generate ExchangeEntry objects for an item depends on the specific needs of the recipie. In most cases a recipie will require a number of a specific item type, in this case you can simply call `GetExchangeEntry` on the specific item.

```csharp
if(itemToExchange.GetExchangeEntry(quantity, out entries))
{
    // Enough where found
}
else
{
    // Not enough of this item available
}
```

Once you have the collection of ExchangeEntries you can pass them into the item you wish to exchange them for.

```
item.Exchange(exchangeEntries, callback);
```

#### Use Cases

Exchange chest for bundle

```csharp
if(chest.GetExchangeEntry(1, out EchangeEntry[] entries))
{
    bundle.Exchange(entries, (result, error) => {
        Debug.Log("result contains the items we gave the player");
    });
}
else
{
    Debug.Log("The player didn't have any chests");
}
```

Exchange 10 iron and 50 gold for 1 ironSword;

```csharp
if(iron.GetExchangeEntry(10, out EchangeEntry[] ironEntries))
{
    if(gold.GetExcahngeEntry(50, out ExchangeEntry[] goldEntries))
    {
        var recipie = new List<ExchangeEntry>();
        recipie.Add(ironEntries);
        recipie.Add(goldEntries);
        ironSword.Exchange(recipie, (result, error) => {
            Debug.Log("results contains the sword if any");
        });
    }
    else
    {
        Debug.Log("Not enough gold");
    }
}
else
{
    Debug.Log("Not enough iron");
}
```

### Generate Items

{% hint style="warning" %}
This is only avialable to developers of this app
{% endhint %}

Grants the player this item, this is used only by developers and is meant for testing only.

```
item.GenerateItem(callback);
```

To generate multiple instances of this item you can use

```
item.GenerateItem(count, callback);
```

### Start Purchase

{% hint style="warning" %}
Only items that have a valid price or price category and are not set to store hidden or hidden in general can be called to start purchase.
{% endhint %}

{% hint style="info" %}
You can use API.Inventory.Client.StartPurchase to start a purchase on a complex cart of items. This example on the Item Defintion is for starting a purchase of a single item or some quantity of a signle item.
{% endhint %}

```
item.StartPurchase(callback);
```

or

```
item.StartPurchse(count, callback);
```

or

```
API.Inventory.Client.StartPurchase(items, itemQuantities, callback);
```
