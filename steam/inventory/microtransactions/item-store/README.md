---
description: Creating an item store in game and in Steam
---

# 🛒 Item Store

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="warning" %}
You cannot test Steam Inventory features with App ID 480 aka Spacewars.

\
To test Steam Inventory features including but not limited to microtransactions, crafting, player inventory, etc. you will need to register for your app ID and configure your own Steam Inventory Items.\
\
As a result of this limitation from Valve, the sample scenes for Inventory cannot be used with App 480 in any functional form.
{% endhint %}

A common request we see is for an example in-game store or other "MTX" (micro-transaction) example.

Since Valve's Spacewar doesn't have a usable Steam Inventory configuration and since your store would be highly dependent on what items you have and how they are configured. The sample scene we have provided (9 Item Store Tutorial) simply contains example scripts based on this article and is meant to be a teaching tool, not a functional example.

This article will describe the concepts of an item store and cover several common use cases providing abstract examples for each. Finally, in the end, we will compile a list of commonly asked questions and of course, if you have any questions please reach out to the community on our [Discord](https://discord.gg/6X3xrRc) server.

## Quick Start

This assumes you have read over the [Microtransactions article](../) and understand how to reference an [Item Definition](../../../../company/steam/steamworks/inventory/#item-definition).

### Step 1: Create the Store UI

Create your Store UI using Unity's UI tools as you would any other UI. The only thing of relevant note is the "button" or other UI elements you will have your users interact with that are meant to put an item in the carte or are meant to "Start Purchase"

### Step 2: Connect the UI to items

For your buttons that are meant to add an item to a shopping cart. You will be using [Heathen's Item Shopping Cart Manager](../../../../assets/steamworks/unity/components/item-shopping-cart-manager.md) so that your button on-click adds the item to that script as defined in that script's documentation article.

For "Start Purchase" see the [How do I start a purchase request?](./#how-do-i-start-a-purchase-request) FAQ below.

### Assumptions

This article assumes you have defined your items already. If you have questions about that see our [Getting Started](../../item-definition-tools.md) article.

This article also assumes you already understand how to create UI and behaviours in Unity. If you have questions there we strongly recommend you check out [this tutorial](https://learn.unity.com/pathway/junior-programmer). It's short and very useful for every Unity developer.

## Creating the Store UI

![](<../../../../.gitbook/assets/image (180) (1) (1).png>)

Creating the visuals is up to you, how you do it doesn't matter and this subject is not impacted at all by Steam API you would do it the same way you would create any UI in your game.

As a common point of reference, we assume you're using Unity's uGUI, in our sample scene you will find a crude example of what this might look like. In the example, we have created a simple UI composite object that includes the following features

* Label\
  This is the name of the item. We recommend you hard code this as it's far more performant and less error-prone than run-time initialization. We will discuss run time initialization in a later article.
* Image\
  In our case, we used a Raw Image so we could use the Heathen Logo without needing to set it up as a sprite. You can use anything here even a 3D render. The visual you apply will be hard coded at development time. Again there is no reason to be doing run time initialization here.
* Quantity Owned\
  In our example, we have a simple number under the label that expresses how many of these items the player owns. This value will be updated at run-time any time the inventory updates.
* Start Purchase Button\
  In our case, we are assuming that all items can be purchased in the Steam Store with real money. So this button will open the overlay to the Steam shopping cart with 1 of these items in the cart.
* Exchange Button\
  In some cases, you may want to use an in-game currency or crafting system or otherwise let your players exchange some items for some other items. To do so you would use the exchange system and this button demonstrates how we would do that.\
  Note this button gets set enabled/disabled at run time based on the existence of an exchange recipe and the player having the required items.

### Example Item Behaviour

This is a simple script included in the 9 Item Store Tutorial folder. It is not an example of best practice it is a simple crude example of updating Unity uGUI UI elements based on the values in an Item Definition.&#x20;

This script will update the quantity owned for each item any time the inventory changes and will update the interactable status of the Exchange button based on rather or not the item has an exchange recipe and the local user owning the required items to perform the exchange.

## F.A.Q

### How do I get the item price?

If you want to fetch the price in the user's currency see: [Current Price](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#currentprice) and [Base Price](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#baseprice). You can check if there is a price at all via [Has Price](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#hasprice).

### How do I set up in-game currency?

Your in-game currency would simply be an inventory item. You would then set up "Exchange" recipes for all the items that can be "purchased" for that currency.

In short in-game currency is simply exchanging X items for Y items. See the [Item Definition Exchange section](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#exchange-1) for more details. You can do a lot with exchange well more than would fit in 1 article so be sure to read up in Valve's documentation as well.

### How do I start a purchase request?

On your Item Definition, you will see a Start Purchase option. A similar method is available on the Data Layer, Scriptable Object and of course in the Inventory API. You simply call this method indicating the number of items you wish to start a purchase with.

* [Item Definition Object Start Purchase](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#start-purchase)
* [Item Data Start Purchase](../../../../assets/steamworks/unity-engine/data-layer/item-data.md#start-purchase)
* [Inventory API Start Purchase](../../../../assets/steamworks/unity-engine/api/inventory.client.md#startpurchase)
* [Item Shopping Cart Start Purchase](../../../../assets/steamworks/unity/components/item-shopping-cart-manager.md#startpurchase)

If the item has a properly formatted price or price category (it cannot have both) then the item will be added to the user's Steam Store cart ready for purchase. The Steam Overlay will open showing the user this cart.

When the user completes the transaction you will be notified in two ways.

1. Transaction Complete Event\
   [On the Inventory Manager](../../../../assets/steamworks/unity/components/inventory-manager.md#evttransactionresponce)\
   [On the Inventory API](../../../../assets/steamworks/unity-engine/api/inventory.client.md#event-steam-micro-transaction-authorization-responce)
2. Inventory Change Event\
   [On the Inventory Manager](../../../../assets/steamworks/unity/components/inventory-manager.md#evtchanged)\
   [On the Inventory API](../../../../assets/steamworks/unity-engine/api/inventory.client.md#event-steam-inventory-result-ready)

### How do get the item count?

[Item Definition's Total Quantity](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#totalquantity) indicates the number of this item the player owns.

### How do I refresh the Inventory?

By refresh, we assume you mean how to get the current count of the user's inventory.

[Inventory API's Get All Items](../../../../assets/steamworks/unity-engine/api/inventory.client.md#getallitems) will do that for you calling its callback when the process is complete.

### Testing Inventory Change

So you have set up your inventory items, your going to use full Client API so you can't simulate an end-to-end purchase. You're asking yourself ... How do I test my game logic to make sure it's handling inventory change correctly?

Use the [Steamworks Inspector](../../../../company/steam/steamworks/#inventory) and click the "Grant" button beside any of the items, this will cause it to grant you an item which will raise the [EventChanged](../../../../assets/steamworks/unity/scriptable-objects/steam-settings/game-client/inventory-settings.md) ... you can now observe your game logic and ensure it's performing as you expected.
