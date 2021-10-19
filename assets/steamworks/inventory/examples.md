---
description: Steamworks Inventory Examples
---

# Examples

## Reading Player Inventory

{% hint style="success" %}
In Steam Inventory each item can have 0 or many item detail instances and each instance can represent a quantity of 0 to many.

Its best to think of a `SteamItemDetails_t` entry as a "stack" of items; each stack may contain none or many of that item.
{% endhint %}

### Quantity and Count

The "view" of the player's inventory is stored on the Item Data objects you created. That is the InventoryItemDefintion objects you created and attached to the Inventory Editor or Inventory Settings object have a Quantity and Sum value on them indicating how many instances of that object the local player owns.

```csharp
//Sum of quantity of all instances this user owns
var quantity = myItem.Sum;

//Number of instances this user owns
var instances = myItem.Count;
```

### Iterating over instances

```csharp
foreach(var instance in myItem)
{
    Debug.Log("Instance id: " + instance.m_itemId 
        + " has a quantity of " + instance.m_unQuantity);
}
```

### Iterating over item types

In general you will check a specific item, but there are cases when you want to iterate over all possible item types.&#x20;

```csharp
foreach(var item in SteamSettings.Client.inventory.itemDefinitions)
{
    ...
}
```

## Refreshing Player Inventory

{% hint style="danger" %}
Remember it is **Steam Inventory** not your game's inventory. Transactions can happen from outside of your game, modifying the state of the inventory at any time, and your game will not necessarily be made aware of these changes when they occur.&#x20;

As such its keenly important that you refresh your game's view of the player's inventory before performing any important action, such as crafting/exchanging, consuming or performing any other action where you need to insure your view of the inventory is fresh.

You should not perform this every frame, in general you only need to perform this when your taking some key action such as opening the player's inventory UI, opening the "Crafting UI" if your game has such, etc.
{% endhint %}

As with many important systems we give you many ways to reach this functionality. All cases perform the same action and ultimately all methods of performing this function call the GetAllItems method on the SteamworksInventoryTools static class

### Static call

```csharp
SteamworksInventoryTools.GetAllItems(...);
```

### From the Client object

```
SteamSettings.Client.RefreshInventory()
```

### From within the Client object

```csharp
SteamSettings.Client.inventory.RefreshInventory();
```

## In Game Purchase

You can start a purchase on one or more items from within your game in a few different ways.

{% hint style="danger" %}
Start Purchase will be ignored on any item that is not properly configured to allow store purchase e.g.&#x20;

* Item must have a "price" or "price\_category" but not both
* Item must **note** be set as "store\_hidden"
* Item must be a true item or bundle not a generator
{% endhint %}

Assuming a start purchase operation is accepted by Steam client, then the Steam Overlay will open with the indicated item or items in the shopping cart. Note that this occurs outside of your game, the user may remove items from the cart, add additional items, cancel the transaction, etc. You do not get an immediate return and may not get any notification of change.

When your game regains focus you will likely want to refresh the player's inventory to insure you have a complete and recent view of what items the player owns.

{% hint style="info" %}
In some cases Steam will raise events that indicate to your game that the inventory has changed. You can respond to these events through the following Unity events.

```csharp
SteamSettings.Client.inventory.evtItemInstancesUpdated
```

This event will provide an array of the SteamItemDetails\_t that where changed. These can be used to look up the item definition if desired e.g.

Keep in mind that this event raises for all changes detected internally by the game including when you refresh the player's inventory. It may also not catch changes from sources such as Player Marketplace. This should be treated as additional data but depended on to maintain an internal view of the inventory.

```csharp
void HandleItemInstancesUpdated(bool error, SteamItemDetail_t[] details)
{
    //Pointer to inventory so the following line can be shorter
    var inventory = SteamSettings.Client.inventory;

    //Iterate over the details
    foreach(var detail in details)
    {
        //Find the item definition if any that matches the detail
        var item = inventory.ItemDefinitions.FirstOrDefault( p =>
            p.definitionID == detail.m_iDefinition);
            
        //If we found one then we know it changed
        if(item != null)
        {
            Debug.Log("Item " + item.name + " quantity changed!");
        }
    }
}
```
{% endhint %}

### Purchase a specific item

On the item definition its self you can simply call&#x20;

{% hint style="info" %}
This is a quick and easy method but lacks a call back. If you want detailed information when the call is completed then you should be using `SteamworksInventoryTools.StartPurchase`
{% endhint %}

```csharp
myItem.StartPurchase(quantity);
```

Assuming myItem points to a valid item or bundle that has been configured correctly, then the Steam Overlay will open with that many of that item in the user's shopping cart.

### Purchase a collection of items

In this case you are asking to purchase multiple items of different types and so should be using the SteamworksInventroyTools object

```csharp
SteamworksInventoryTools.StartPurchase(itemsToPurchase,
    callback);
```

items to purchase should be an enumerable collection such as a List or array of `InventoryItemDefinitionCount` this is a custom object that expresses which item and how many of it. The final parameter callback is optional and is simply a method to be invoked when the operation is completed. This callback will be called by Valve when the purchase results are resolved and will include the order ID and transaction ID.

Assuming this transaction resulted in a change of inventory this should also raise the `evtItemInstancesUpdated` event as noted above, this event will indicate what items where modified.

## Crafting / Item Exchange

Steam Inventory lets you exchange one or more items for another item. This can be used to create crafting systems, loot box systems or even item upgrade systems.

This is handled by defining "recipes" for our items. In Heathen's Steamworks SDK you can create a recipe by right clicking in your project folder and selecting&#x20;

`Create > Steamworks > Crafting Recipie`

This will create a new Crafting Recipe object where you can define what "ingredients" are required to satisfy this recipe, you can now drag this recipe to any given item's recipe slot to associate the recipe with that item, meaning that this recipe can be used to "craft" this item.

![](<../../../.gitbook/assets/image (66).png>)

{% hint style="info" %}
An item can have multiple recipes
{% endhint %}

### Use Cases

#### Crafting System

In this use case we would define recipes for the items that can be crafted. You would of course also need to define the reagents required e.g. the materials/ingredients.

#### Upgrade System

This is like a crafting system, the major difference being that a lesser version of the item is part of its recipe. For example you may require 2 iron bars + some gold coins + a common Iron Sword as ingredients in creating an uncommon Iron Sword.

## Consuming Items

Consuming an item means to remove it from the player's inventory e.g. to destroy it. This is usually done for "consumables" such as potions, food or other one time use items hence the name of the method `consume` . to do so simply call `Consume` on your item.

### Consume a quantity

```csharp
item.Consume(1);
```

This will simply consume the indicated number of instances if that quantity is available. This will work against the available instances the player owns in the order they are loaded.

### Consume from an instance

```csharp
item.Consume(instance, 1);
```

This will consume the quantity indicated from the specified instance. Remember an instance is like a stack of items and may contain 0 to many quantity of that item type. An instance is most commonly thought of as a stack of said item.
