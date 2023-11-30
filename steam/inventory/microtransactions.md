---
description: Aka MTX, IAP, In App Purchase, cash shop, etc.
---

# 💸 Microtransactions

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Steam Microtransactions (In-Game Purchases) are handled via the [Steam Inventory](../../company/steam/steamworks/inventory/) feature.&#x20;

{% hint style="info" %}
Have a look at our articles on [Monetization ](../../company/design/monetization/)before you get started designing your game's monetization systems.&#x20;

[https://kb.heathenengineering.com/company/concepts/monetization](https://kb.heathenengineering.com/company/concepts/monetization)
{% endhint %}

{% hint style="warning" %}
You cannot test Steam Inventory features with App ID 480 aka Spacewars.

\
To test Steam Inventory features including but not limited to microtransactions, crafting, player inventory, etc. you will need to register for your app ID and configure your own Steam Inventory Items.\
\
As a result of this limitation from Valve, the sample scenes for Inventory cannot be used with App 480 in any functional form.
{% endhint %}

A common request we see is for an example in-game store or other "MTX" (micro-transaction) example.

Valve's Spacewar doesn't have a usable Steam Inventory configuration and since your store would be highly dependent on what items you have and how they are configured. The sample scene we have provided (9 Item Store Tutorial) simply contains example scripts based on this article and is meant to be a teaching tool, not a functional example.

This article will describe the concepts of an item store and cover several common use cases providing abstract examples for each. Finally, in the end, we will compile a list of commonly asked questions and of course, if you have any questions please reach out to the community on our [Discord](https://discord.gg/6X3xrRc) server.

## In-Game Currency

Your in-game currency would simply be an inventory item. You would then set up "Exchange" recipes for all the items that can be "purchased" for that currency.

In short in-game currency is simply exchanging X items for Y items. See the [Crafting System](crafting-system.md) article for more information on exchanging items.

## Unity Examples

### Testing Inventory Change

So you have set up your inventory items, You are going to use full Client API so you can't simulate an end-to-end purchase. You're asking yourself ... How do I test my game logic to make sure it's handling inventory change correctly?

Use the [Steamworks Inspector](../../company/steam/steamworks/#inventory) and click the "Grant" button beside any of the items, this will cause it to grant you an item which will raise the [EventChanged](../../heathens-steamworks-complete/unity/scriptable-objects/steam-settings/game-client/inventory-settings.md) ... you can now observe your game logic and ensure it's performing as you expected.

### Start Purchase

This is done when you want to send the user to the Steam Store page so they can "check out" spending real money on some item. Note you can call Start Purchase on a single item or you can set up a shopping cart building up a collection of items and call Start Purchase on all of them.

#### [Item Shopping Cart Manager](../../heathens-steamworks-complete/unity/components/item-shopping-cart-manager.md)

We have constructed a tool to help you manage a shopping cart in the game. This tool is capable of adding, removing and editing the quantities of items in it, it can report the estimated total of the cart and can manage and track the purchase operation through authorization reporting issues and or successes through simple Unity events.

You would add this script to your Store/Shop UI and use its members to add, remove and edit the items in the cart. Once you have populated the cart and are ready to "check out" you can call StartPurchase in the manager to kick off the process and track the results. To learn more about the use of [Item Shopping Cart Manager see this article](../../heathens-steamworks-complete/unity/components/item-shopping-cart-manager.md).

#### Manual

On your Item Definition, you will see a Start Purchase option. A similar method is available on the Data Layer, Scriptable Object and of course in the Inventory API. You simply call this method indicating the number of items you wish to start a purchase with.

* [Item Definition Object Start Purchase](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md#start-purchase)
* [Item Data Start Purchase](../../heathens-steamworks-complete/unity/data-layer/item-data.md#start-purchase)
* [Inventory API Start Purchase](../../heathens-steamworks-complete/unity/api/inventory.client.md#startpurchase)
* [Item Shopping Cart Start Purchase](../../heathens-steamworks-complete/unity/components/item-shopping-cart-manager.md#startpurchase)

If the item has a properly formatted price or price category (it cannot have both) then the item will be added to the user's Steam Store cart ready for purchase. The Steam Overlay will open showing the user this cart.

When the user completes the transaction you will be notified in two ways.

1. Transaction Complete Event\
   [On the Inventory Manager](../../heathens-steamworks-complete/unity/components/inventory-manager.md#evttransactionresponce)\
   [On the Inventory API](../../heathens-steamworks-complete/unity/api/inventory.client.md#event-steam-micro-transaction-authorization-responce)
2. Inventory Change Event\
   [On the Inventory Manager](../../heathens-steamworks-complete/unity/components/inventory-manager.md#evtchanged)\
   [On the Inventory API](../../heathens-steamworks-complete/unity/api/inventory.client.md#event-steam-inventory-result-ready)

```csharp
public void StartPurchase()
{
    itemDefinition.StartPurchase((responce, ioError) =>
    {
        if (!ioError)
        {
            if (responce.m_result == EResult.k_EResultOK)
            {
                Debug.Log("Start purchase completed");
                //You should store the order ID if you want to track its completion
                StoreController.orderId = responce.m_ulOrderID;
            }
            else
            {
                Debug.LogError("Unexpected result from Valve: " + responce.m_result);
            }
        }
        else
        {
            Debug.LogError("Valve indicated an IO Error occured. i.e. failed to start the process at all.");
        }
    });
}
```

You can also start purchase on a set of items, the following is the code from our Shopping Cart tool and how it handles this use case.

```csharp
//Remove any empty or null items
items.RemoveAll(p => p.item == null || p.quantity <= 0);
//Create a buffer for the item types
var itemDefs = new Steamworks.SteamItemDef_t[items.Count];
//A buffer for the item quantities
var itemQuan = new uint[items.Count];
//Populate the buffers from our cart
for (int i = 0; i < items.Count; i++)
{
    var entry = items[i];
    itemDefs[i] = entry.item.Id;
    itemQuan[i] = entry.quantity <= 0 ? 0 : (uint)(entry.quantity);
}
//Start the purcahse
API.Inventory.Client.StartPurchase(itemDefs, itemQuan, (result, error) =>
{
    if(error)
    {
        //Report the IO Error
        Debug.LogError($"StartPurchase - IO Error reported by Steam");
        evtStartPurchaseError.Invoke(EResult.k_EResultIOFailure);
    }
    else
    {
        if (result.m_result != EResult.k_EResultOK)
        {
            //Report the Result Error
            Debug.LogError($"StartPurchase - Error reported by Steam: {result.m_result}");
            evtStartPurchaseError.Invoke(result.m_result);
        }
        else
        {
            //Record the result so we can process the auth responce later
            _result = result;
            evtStartPurchaseSuccess.Invoke(result);
        }
    }

    callback?.Invoke(result, error);
});
```

Assuming you want to track the completion of the order you should listen on the Micro Transaction Authorization Response. You can find this on the [Inventory Manager](../../heathens-steamworks-complete/unity/components/inventory-manager.md#evttransactionresponce) component or directly in the [Inventory API](../../heathens-steamworks-complete/unity/api/inventory.client.md#eventsteammicrotransactionauthorizationresponce). In either case, this is an event that is raised when the Steam client informs your game of a completed e.g. authorization on a transaction. The event will indicate the app the transaction is for, the order ID of the transaction and rather or not the transaction was authorized.

### Exchange

It's fairly common to have users "purchase" items with an in-game currency. In reality, this is not a purchase it is an exchange. That is it is similar to crafting where some reagents are exchanged for some other item. Exchanges must be done one item at a time and the following code snippet shows how you would go about doing that for a given [itemDefinition](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md).

```csharp
public void Exchange()
{
    //This assumes the linked item has a recipe
    if (itemDefinition.CanExchange(itemDefinition.item_exchange.recipe[0], out List<ExchangeEntry> recipe))
    {
        //If the user owns the required items to satisfy the recipe defined in the first index of the recipies 
        //then go ahead and exchange for it

        itemDefinition.Exchange(recipe, (responce) =>
        {
            if (responce.result == EResult.k_EResultOK)
            {
                Debug.Log("Exchange completed");
            }
            else
            {
                Debug.LogError("Unexpected result from Valve: " + responce.result);
            }
        });
    }
    else
    {
        Debug.LogWarning("The user does not own the required items to perform this exchange");
    }
}
```

The first step in this process is the CanExchange check.

```csharp
if (itemDefinition.CanExchange(itemDefinition.item_exchange.recipe[0],
                               out List<ExchangeEntry> recipe))
```

[CanExchange ](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md#can-exchange)is a method on the [Item Definition](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md) that takes a given recipe as an input and has an output that collects the required items to complete the recipe.

Assuming this returns true then we can complete an exchange for this item on this recipe, so the next step is to request that using the output the [CanExchange](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md#can-exchange) method provided us. Unlike StartPurchase we will know in a single step whether or not this was a success and the items will already be updated.

### Get Item Price

If you want to fetch the price in the user's currency see: [Current Price](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md#currentprice) and [Base Price](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md#baseprice). You can check if there is a price at all via [Has Price](../../heathens-steamworks-complete/unity/scriptable-objects/item-definition.md#hasprice).

## Unreal Examples

### Testing Inventory Change

The [Inventory Results Ready event](../../heathens-steamworks-complete/unreal/blueprint-nodes/events/inventory-results-ready.md) can be used to know when the player's inventory has changed. This will be raised by Steam for any change caused by the game but may not be raised in response to changes that start outside the game so it's important to not use this as an alternative to [Get All Items](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/get-all-items.md) for keeping your view of the player's inventory up to date.

### Start Purchase

The Start Purchase function asks Steam to load a shopping cart with given items and present it to the user for payment processing. Only items that have a defined price can be purchased, only items available to this user can be purchased. Steam will process the payment from that point forward and you are not assured of getting a response. For example, a player may simply leave the cart open and never process the transaction, they may cancel the transaction, modify items in the cart, etc.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

If a transaction is processed and authorized you will see a [Micro Txn Authorization Response](../../heathens-steamworks-complete/unreal/blueprint-nodes/events/micro-txn-authorization-response.md) event be executed. That event will carry the Order ID which can be matched to the Order ID created with the Start Purchase request.

<figure><img src="../../.gitbook/assets/image (373).png" alt=""><figcaption></figcaption></figure>

### Exchange

[Exchange Items](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/exchange-items.md) lets you pass in an array of [Item Count](../../heathens-steamworks-complete/unreal/blueprint-nodes/types/item-count.md) to exchange for a given item. The callback works much like the [Get All Items](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/get-all-items.md) discussed in the [Inventory](../../company/steam/steamworks/inventory/) article.

To use the feature you first need to know what item ID you want to "craft" i.e. exchange other items for.&#x20;

Next, you need to know the instance ID and count of each item you will be exchanging. You typically get the Instance IDs from the Get All Items request but you can for example cascade crafting requests.

An example of a cascaded crafting request would be to craft Iron Ore into Iron Bars and then craft the Iron Bars into an Iron Sword. That is your exchanging 1 or more Ore items for Bars and 1 or more Bars for Sword.

The following image is an example of creating the "recipe" array needed by the Exchange Items node. In this example, we assumed we needed 15 of some item and if we had 2 stacks of 10 each with IDs of 123 and 124 respectively then the below "Make Array" node would be the correct recipe.

In the example, we are using all of stack 123 and 5 from stack 124.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

### [Get Item Price](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/get-item-price.md)

If you are setting up an in-game store or some similar microtransaction system you will likely want to know what the price of the item is for this user.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Notice that the event tells you the currency code and currency symbol seen for the user and that prices are returned as a whole number e.g. int64

In the case of say USD you would want to convert the price to a float and divide by 100 so that 199 becomes 1.99\
\


<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

The above are the relevant nodes to yield a string formatted for the user's currency assuming a cent-based currency like USD, GBP, etc. The resulting string here would look like this \`$1.99" assuming a base price of 199 and a currency symbol of $
