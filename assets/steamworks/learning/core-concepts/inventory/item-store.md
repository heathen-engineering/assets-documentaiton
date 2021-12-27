# Item Store

## Introduction

A common request we see is for an example in-game store or other "MTX" (micro-transcation) example.

Since Valve's Spacewar doesn't have a usable Steam Inventory configuraiton and since your store would be highly dependent on what items you have and how they are configured. The sample scene we have provided (9 Item Store Tutorial) simply contains example scripts based on this article and is meant to be a teaching tool not a funcitonal exmaple.

This article will discribe the concepts of an item store and cover several common use cases providing abstract examples for each. Finally at the end we will compile a list of commonly asked questions and of course if you have any questions please reach out to the community on our [Discord](https://discord.gg/6X3xrRc) server.

### Assumptions

This article assumes you have defined your items already. If you have questions about that see our [Getting Started](../../../features/inventory/getting-started.md) article.

This article also assumes you already understand how to create UI and behaviours in Unity. If you have questions there we strongly recomend you check out [this tutorial](https://learn.unity.com/pathway/junior-programmer). Its short and very useful for every Untiy developer.

## Creating the Store UI

![](<../../../../../.gitbook/assets/image (180).png>)

Creating the visuals is up to you, how you do it doesn't really matter and this subject is not impacted at all by Steam API you would do it the same way you would create any UI in your game.

As a common point of reference we assume your using Unity's uGUI, in our sample scene you will find a crude example of what this might look like. In the example we have created a simple UI composit object that includes the following features

* Lable\
  This is the name of the item. We recomend you hard code this as its far more performant and less error prone than run time initalization. We will discus run time initalization in a later article.
* Image\
  In our case we used a Raw Image so we could use the Heathen Logo without needing to set it up as a sprite. You can use anything here even a 3D render. The visual you apply will be hard coded at development time. Again there is no reason to be doing run time initalizaiton here.
* Quantity Owned\
  In our example we have a simple number under the label that expresses how many of this item the player owns. This value will be updated at run time any time the inventory updates.
* Start Purchase Button\
  In our case we are assuming that all items can be purchased in the Steam Store with real money. So this button will open the overlay to the Steam shoping cart with 1 of these items in the cart.
* Exchange Button\
  In some cases you may want to use an in-game currency or crafting system or otherwise let your player's exchange some items for some other item. To do so you would use the exchange system and this button demonstrates how we would do that.\
  Note this button gets set enabled/disbaled at run time based on the existance of an exchange recipie and the player haveing the required items.

### Example Item Behaviour

This is a simple script included in the 9 Item Store Tutorial folder. It is not an example of best practice it is a simple crude example of updating Unity uGUI UI elements based on the values in an Item Definition.&#x20;

This script will update the quantity owned for each item any time the inventory changes and will update the interactable status of the Exchange button based on rather or not the item has an exchange recipie and the local user owning the required items to perform the exchange.

## Run Time Initalization

{% hint style="danger" %}
We strongly recomend against run time initalization of Steam Inventory.

\
You already know every item your game will have, that items name, its visuals, etc. at development time. Unless your game supports you adding and modifying items without patching the game; then there is no reason to use run time initalizaiton.

\
Draw backs to run time initalization

1. Error prone\
   Any process can fail and will fail for some users some times
2. Slower\
   It extends load time for your users, for users on slow networks it can drasticly slow load times
3. Memory use\
   Loading images and the likes at run time is nearly always less memory performant than doing so at dev time where unity can compres and organize your assets

\
Benifits

None that cant be done better with other methods.
{% endhint %}

With that out of the way the following sections discribe how you would go about initalizing items at run time.

### Step 1: Load Item Definitions

```csharp
API.Inventory.Client.LoadItemDefinitions();
```

Read more [here](../../../api/inventory.md#loaditemdefinitions).

In short this starts the process of loading item definitions from Steam and will trigger the [EventSteamInventoryDefinitionUpdate](../../../api/inventory.md#eventsteaminventorydefinitionupdate) to be raised when the definitions are ready.

You would do this as soon as Steam Initalizes so you can pull the current item defintions local.

### Step 2: Iterate and Initalize

Once the [EventSteamInventoryDefinitionUpdate ](../../../api/inventory.md#eventsteaminventorydefinitionupdate)has been raised and you have the item defintions local to the user's cash you can walk the items and spawn UI objects to represent each.

```csharp
foreach(var itemDefinition in SteamSettings.Client.inventory.items)
{
    //Instantiate your UI here for this item
}
```

For each item you will need to get some common information.&#x20;

* Item Name\
  You can find this in item\_name. or by using the DisplayName field of Item Defintion.
