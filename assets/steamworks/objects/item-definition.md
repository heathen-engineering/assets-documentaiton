---
description: Defines a Steam Inventory Item
---

# Item Definition

## Definition

```csharp
public class ItemDefinition : ScriptableObject
```

Represents a Steam Inventory Item of any type. This object contains all the schema data for any possible item. The specifics of each field are defined in [Steam's Inventory Schema documentaiton](https://partner.steamgames.com/doc/features/inventory/schema).

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

This document will not reiterate the Schema fields those are detailed in Valve's documentation. The fields listed here are in addition to and are used during run time to manage the items owned by the player that this definition represents.

## Fields and Attributes

| Type                                                 | Name                         | Comment                                                                                                                                                                                                            |
| ---------------------------------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SteamItemDef\_t                                      | Id                           | The id of the item and used by most API.Inventory interface features                                                                                                                                               |
| List<[ItemDetail](item-details.md)>                  | Details                      | <p>A list of Steam Item Instance's of this item type owned by the local player.</p><p></p><p>This contains additional data about the item instance including ItemProperty[], dynamic properties and item tags.</p> |
| long                                                 | TotalQuantity                | The sum of the quantities in each Item Detail                                                                                                                                                                      |
| [InventoryItemType](../enums/inventory-item-type.md) | item\_type                   | The type of item ... used when serializing                                                                                                                                                                         |
| Language Variant Node                                | item\_name                   | the name of the item ... used when serializing                                                                                                                                                                     |
| Language Variant Node                                | item\_description            | The description of the item ... used when serializing                                                                                                                                                              |
| Language Variant Node                                | item\_display\_type          | The display type of the item ... used when serializing                                                                                                                                                             |
| int                                                  | item\_itemdefid              | The unique ID of this item in this app ... used when serializing                                                                                                                                                   |
| Bundle                                               | item\_bundle                 | The bundle definition for this item if any ... used when serializing                                                                                                                                               |
| PromoRule                                            | item\_promo                  | The promotion defintion rules for this item if any ... used when serializing                                                                                                                                       |
| string                                               | item\_drop\_start\_time      | The item drop start time if this is a promo item ... used when serializing                                                                                                                                         |
| ExchangeCollection                                   | item\_exchange               | The exchange recipies for this item if any ... used when serializing                                                                                                                                               |
| Price                                                | item\_price                  | The item price for this item if any ... used when serializing                                                                                                                                                      |
| Color                                                | item\_background\_color      | The item backaground color ... used when serializing                                                                                                                                                               |
| Color                                                | item\_name\_color            | The item name color ... used when serialzing                                                                                                                                                                       |
| string                                               | item\_icon\_url              | The item icon URL if any ... used when serializing                                                                                                                                                                 |
| string                                               | item\_icon\_url\_large       | The item large icon URL if any ... used when serialzing                                                                                                                                                            |
| TagCollection                                        | item\_tags                   | The item tag collection if any ... used when serializing                                                                                                                                                           |
| List\<ItemDefinition>                                | item\_tag\_generators        | The collection of related tag generators for this item if any ... used when serializing                                                                                                                            |
| string                                               | item\_tag\_generator\_name   | The tag generator name if any ... used when serializing                                                                                                                                                            |
| List\<string>                                        | item\_store\_tags            | Collection of store tags if any ... used when serializing                                                                                                                                                          |
| List\<string>                                        | item\_store\_images          | Collection of image URLs for store images if any ... used when serializing                                                                                                                                         |
| bool                                                 | item\_hidden                 | Is this a hidden item ... used when serializing                                                                                                                                                                    |
| bool                                                 | item\_store\_hidden          | Is this item hidden in the store ...  used when serializing                                                                                                                                                        |
| bool                                                 | item\_use\_drop\_limit       | Does this item use drop limit ... use when serializing                                                                                                                                                             |
| uint                                                 | item\_drop\_limit            | used when serializing                                                                                                                                                                                              |
| uint                                                 | item\_drop\_interval         | used when serializing                                                                                                                                                                                              |
| bool                                                 | item\_use\_drop\_window      | used when serializing                                                                                                                                                                                              |
| uint                                                 | item\_drop\_window           | used when serializing                                                                                                                                                                                              |
| uint                                                 | item\_drop\_max\_per\_window | used when serializing                                                                                                                                                                                              |
| bool                                                 | item\_granted\_manually      | used when serializing                                                                                                                                                                                              |
| bool                                                 | item\_use\_bundle\_price     | used when serializing                                                                                                                                                                                              |
| bool                                                 | item\_auto\_stack            | used when serializing                                                                                                                                                                                              |
| ExtendedSchema                                       | item\_extendedSchema         | used when serializing                                                                                                                                                                                              |

## Methods

### Add Promo Item

```csharp
public bool AddPromoItem(callback);
```

Grants the item in a one-time promotional to the local user

### Get Consume Orders

```csharp
public ConsumeOrder[] GetConsumeOrders(quantity);
```

Creates ConsumeOrders which can be used with the Consume method to consume instances of this item if available. This is only needed when consuming more than 1 instance at a time.

### Consume

```csharp
public bool Consume(callback);
```

```csharp
public bool Consume(order, callback);
```

Consume 1 or many instances of this item if the player owns them

### Can Exchange

This method checks if a user can exchange for this item using a specific recipie. You can get the list of available recipies from the ItemDefinition.item\_exchange or you can create the recipie manually if you know the items needed.

{% hint style="info" %}
This will always return false if the recipie uses tags in any of the required items
{% endhint %}

```csharp
public bool CanExchange(ExchangeRecipe, out List<ExchangeEntry>);
```

### Get Exchange Entry

```csharp
public bool GetExchangeEntry(quantity, out entries);
```

Gets a set of ExchangeEntry objects that match the quantity provided if the player's owns them. This can be used with Exchange to "craft" 1 item by exchanging a set of other items.

### Exchange

Exchanges a collection of ExchangeEntry for this item. The Valve backend will validate and insure that this set of ExchangeEntries satisifies one of the configured excahnge recipies for this item.

```csharp
public void Exchange(IEnumerable<ExchangeEntry>, callback);
```

Exchanges a set of ExchangeEntry objects to create a new instance of this item.

### Generate Item

{% hint style="warning" %}
Can only be used by developers for development testing
{% endhint %}

```csharp
public void GenerateItem(callback);
```

Only available to developers, this simply creates a new instance of this item

### Start Purchase

```csharp
public void StartPurchase(callback);
```

If the item is confugred correctly for store purchases this will open the store loading the cart with the indicated number of items to be purcahsed.

### Trigger Drop

```csharp
public void TriggerDrop(callback);
```

Triggers a play time drop assuming the player has played long enough and the item is a playtime generator item.

## How To

### Check Ownership

{% hint style="info" %}
First you need to make sure you have loaded the user's inventory. This is probably already done for  you in that the Heathen Steamworks Behaviour will call GetAllItems when it first initalizes however its important to understand that Steam Inventory can change from many different points of view both in and out of game so to be sure you have the latest we do sugest you refresh your local view of the user's inventory jsut before you preform any sinsative tasks.
{% endhint %}

Once your happy that the local state is fresh enough for your purposes you can check for ownership of an item by simply checking its TotalQuantity

```csharp
if(item.TotalQuantity > 0)
    Debug.Log("The user owns " + item.TotalQuanity + " of this item.");
else
    Debug.Log("The user does not own any of this item.");
```

### Refresh Inventory

You can refresh the local state of items at any time, keep in mind Valve may rate limit this and simply return the most recent cashe value.

To refresh the full inventory&#x20;

```csharp
API.Inventory.Client.GetAllItems(callback);
```

The callback is optional and can be used to know when the results comeback. The Heathen SteamSettings object will update the state of all known ItemDefinition objects so its not nessisary to process the resulting InventoryResults object unless you want to check for something specific.

You can also choose to refresh a specific set of item instances

```csharp
API.Inventory.Client.GetItemsByID(instances, callback);
```

As with GetAllItems the callback is optional and can be used to check the specifics of the resullting data or simply to know when the request has been completed.

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

Exchange for a particular recipie;

In this use case we pick a particular recipie for the item we want to exchange ... lets say we want to exchange 10 gold and 1 gem for a random item. Lets assue our random item is defined as an item generator named randomLoot;

Lets allso assume that the recipie to do this is the first recipie in our randomLoot item.

```csharp
var recipie = randomLoot.item_exchange.recipie[0];

if(randomLoot.CanExchange(recipie, out List<ExchangeEntry> entries))
{
    //This returns true if the local user owns the required items
    //We can use the output entries to execute the exchange
    randomLoot.Exchange(entries, (responce) =>
    {
        if(responce.result == EResult.k_EResultOK)
            Debug.Log("Complete");
        else
            Debug.LogWarning("Something went wrong ... check the result");
    });
}
```

Exchange 10 iron and 50 gold for 1 ironSword;

In this example we will manually build out the exchange entries checking each one as we go.

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

### Generate or Grant Items

{% hint style="warning" %}
From the Client API this is only avialable to developers of this app for development testing. If you need to do this in production for a non-developer then you need to use the [Web API](https://partner.steamgames.com/doc/webapi/IInventoryService).
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
