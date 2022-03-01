# Item Store

## Introduction

{% hint style="warning" %}
You cannot test Steam Inventory features with App ID 480 aka Spacewars.

\
In order to test Steam Inventory features including but not limited to microtransactions, crafting, player inventory, etc. you will need to register your for your own app ID and configure your own Steam Inventory Items.\
\
As a result of this limitation from Valve the sample scenes for Inventory cannot be used with App 480 in any functional form.
{% endhint %}

A common request we see is for an example in-game store or other "MTX" (micro-transaction) example.

Since Valve's Spacewar doesn't have a usable Steam Inventory configuration and since your store would be highly dependent on what items you have and how they are configured. The sample scene we have provided (9 Item Store Tutorial) simply contains example scripts based on this article and is meant to be a teaching tool not a functional example.

This article will describe the concepts of an item store and cover several common use cases providing abstract examples for each. Finally at the end we will compile a list of commonly asked questions and of course if you have any questions please reach out to the community on our [Discord](https://discord.gg/6X3xrRc) server.

### Assumptions

This article assumes you have defined your items already. If you have questions about that see our [Getting Started](../../../features/inventory/getting-started.md) article.

This article also assumes you already understand how to create UI and behaviours in Unity. If you have questions there we strongly recommend you check out [this tutorial](https://learn.unity.com/pathway/junior-programmer). Its short and very useful for every Unity developer.

## Creating the Store UI

![](<../../../../../.gitbook/assets/image (180).png>)

Creating the visuals is up to you, how you do it doesn't really matter and this subject is not impacted at all by Steam API you would do it the same way you would create any UI in your game.

As a common point of reference we assume your using Unity's uGUI, in our sample scene you will find a crude example of what this might look like. In the example we have created a simple UI composite object that includes the following features

* Label\
  This is the name of the item. We recommend you hard code this as its far more performant and less error prone than run time initialization. We will discus run time initialization in a later article.
* Image\
  In our case we used a Raw Image so we could use the Heathen Logo without needing to set it up as a sprite. You can use anything here even a 3D render. The visual you apply will be hard coded at development time. Again there is no reason to be doing run time initialization here.
* Quantity Owned\
  In our example we have a simple number under the label that expresses how many of this item the player owns. This value will be updated at run time any time the inventory updates.
* Start Purchase Button\
  In our case we are assuming that all items can be purchased in the Steam Store with real money. So this button will open the overlay to the Steam shopping cart with 1 of these items in the cart.
* Exchange Button\
  In some cases you may want to use an in-game currency or crafting system or otherwise let your player's exchange some items for some other item. To do so you would use the exchange system and this button demonstrates how we would do that.\
  Note this button gets set enabled/disabled at run time based on the existence of an exchange recipe and the player having the required items.

### Example Item Behaviour

This is a simple script included in the 9 Item Store Tutorial folder. It is not an example of best practice it is a simple crude example of updating Unity uGUI UI elements based on the values in an Item Definition.&#x20;

This script will update the quantity owned for each item any time the inventory changes and will update the interactable status of the Exchange button based on rather or not the item has an exchange recipe and the local user owning the required items to perform the exchange.

## Run Time Initialization

This means having your game's logic iterate over Steam Settings and building out the list of items at run time.

{% hint style="danger" %}
We strongly recommend against run time initialization of Steam Inventory.

\
You already know every item your game will have, that items name, its visuals, etc. at development time. Unless your game supports you adding and modifying items without patching the game; then there is no reason to use run time initialization.

\
Draw backs to run time initialization

1. Error prone\
   Any process can fail and will fail for some users some times
2. Slower\
   It extends load time for your users, for users on slow networks it can drastically slow load times
3. Memory use\
   Loading images and the likes at run time is nearly always less memory performant than doing so at dev time where unity can compress and organize your assets

\
Benefits

None that cant be done better with other methods.
{% endhint %}

With that out of the way the following sections describe how you would go about initializing items at run time.

### Step 1: Load Item Definitions

```csharp
API.Inventory.Client.LoadItemDefinitions();
```

Read more [here](../../../api/inventory.client.md#loaditemdefinitions).

In short this starts the process of loading item definitions from Steam and will trigger the [EventSteamInventoryDefinitionUpdate](../../../api/inventory.client.md#eventsteaminventorydefinitionupdate) to be raised when the definitions are ready.

You would do this as soon as Steam Initializes so you can pull the current item definitions local.

### Step 2: Iterate and Initialize

Once the [EventSteamInventoryDefinitionUpdate ](../../../api/inventory.client.md#eventsteaminventorydefinitionupdate)has been raised and you have the item definitions local to the user's cash you can walk the items and spawn UI objects to represent each.

```csharp
foreach(var itemDefinition in SteamSettings.Client.inventory.items)
{
    //Instantiate your UI here for this item
}
```

For each item you will need to get some common information.&#x20;

* Item Name\
  You can find this in [item\_name](../../../objects/item-definition.md#item\_name). or by using the [DisplayName](../../../objects/item-definition.md#displayname) field of Item Definition.
* Item Description\
  You can find this in [item\_description](../../../objects/item-definition.md#item\_description).
* Price\
  If you want to fetch the price in the user's currency see: [Current Price](../../../objects/item-definition.md#currentprice) and [Base Price](../../../objects/item-definition.md#baseprice). You can check if there is a price at all via [Has Price](../../../objects/item-definition.md#hasprice).
* Images\
  Several images can be associated with an item ... we don't recommend using any of them as they should all be optimized for use in web and thus of pore quality for use in game. but you can read them from the item definition via
  * Icon URL\
    `itemDef.item_icon`\_`url`
  * Large Icon URL\
    `itemDef.item_icon_url_large`
  * Store  Images\
    `foreach(var imageUrl in itemDef.item_store_images)`
* Recipies\
  To detect if this item can be exchanged for and if so what it requires you need to read the [item\_exchange](../../../objects/item-definition.md#item\_exchange).

### Step 3: Start Purchase / Exchange

So now you have your items listed and displaying relevant visuals and information. You now need to respond to use input to start a purchase with real currency or to exchange in-game items aka in-game currency.

You can see a simple working example of this in the Example Item Behaviour.

#### Start Purchase

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

#### Exchange

```csharp
public void Exchange()
{
    //This assumes the linked item has a recipie
    if (itemDefinition.CanExchange(itemDefinition.item_exchange.recipe[0], out List<ExchangeEntry> recipie))
    {
        //If the user owns the required items to satisfy the recipie defined in the first index of the recipies 
        //then go ahead and exchange for it

        itemDefinition.Exchange(recipie, (responce) =>
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

### Step 4: Update

So now you need to insure your UI respond to changes in the inventory rather its a result from a purchase or exchange or some action that happened from outside your game.

Note you don't get clear information in the Client API when a transaction is completed. Start Purchase simply opens the cart, the user may edit that cart, cancel the transaction, etc. and your game will not know.

Similarly the player may purchase items for your game from outside your game while your game is running. Thus you cannot depend on process flow to know when new items are acquired or not.

In general you will either use a "refresh" model where you refresh all items at key points such as when opening the inventory screen

```csharp
API.Inventory.Client.GetAllItems();
```

and you will update your UI anytime the EventSteamInventoryResultReady is raised.

```csharp
private void Start()
{
    //Update the quantity and exchange button ... we dont use the param but need it for the listener so just pass in default here
    RefreshItem(default);

    //This occurs for many reasons including any changes or query of any items.
    //We can use this to refresh the quantity
    InventoryAPI.EventSteamInventoryResultReady.AddListener(RefreshItem);
}

private void OnDestroy()
{
    //We should always clear listeners that are no longer valid or needed
    InventoryAPI.EventSteamInventoryResultReady.RemoveListener(RefreshItem);
}
```

In short you do not update your UI every frame as that will adversely impact game performance instead you listen for the EventSteamInventoryResultReady event and update your UI with it.

## F.A.Q

### How do I list my items?

By list your items I assume your asking how does your game know what items there are so it can update the UI for them.

This suggests that your planning on a [run time initalization](item-store.md#run-time-initalization), please read that section and understand why its not recommended.

To answer that question in short, you created the items, you already know what they are, you do not need to iterate over a list and have it create the UI at run time. If you want to have it do it at run time for some reason the items you created are defined in your Steam Settings as Scriptable Objects so you simply need to iterate over [that list](../../../objects/steam-settings/game-client/inventory-settings.md).

You could also use the [Inventory Manager](../../../components/inventory-manager.md) to fetch those items, it includes a method to get a sub set of all the items which represent those items that are [valid store items](../../../components/inventory-manager.md#getstoreitems).

### How do I get item price?

In general we avoid showing the price in game or if we must we show a fixed known price as opposed to trying to get the user's local price.

Remember your user could be anywhere, using any of Steam's supported currencies and its not always possible to know what currency they are using in the Steam client.

That said:

If you want to fetch the price in the user's currency see: [Current Price](../../../objects/item-definition.md#currentprice) and [Base Price](../../../objects/item-definition.md#baseprice). You can check if there is a price at all via [Has Price](../../../objects/item-definition.md#hasprice).

### How do I set up in-game currency?

Your in-game currency would simply be an inventory item. You would then set up "Exchange" recipes for all the items that can be "purchased" for that currency.

In short in-game currency is simply exchanging X items for Y item. See the [Item Defintion Exchange section](../../../objects/item-definition.md#exchange-1) for more details. You can do a lot with exchange well more than would fit in 1 article so be sure to read up in Valve's documentation as well.

### How do get item count?

[Item Defintion's Total Quantity](../../../objects/item-definition.md#totalquantity) indicates the number of this item the player owns.

### How do I refresh the Inventory?

By refresh we assume you mean how to get the current count of the user's inventory.

[Inventory API's Get All Items](../../../api/inventory.client.md#getallitems) will do that for you calling its callback when the process is complete.

### How do I test purchasing

This depends somewhat in what you mean by "store purchase". Steam Inventory can be used to drive microtransactions in several different forms. For example you can use the Web API coupled with Steam Inventory to handle transactions your self and grant items.&#x20;

To learn more about your opens read this article

{% embed url="https://partner.steamgames.com/doc/features/microtransactions/implementation" %}

For the sake of simplicity lets assume your using Client API only to Start Purchase on an item. This method doesn't require any Web API or any other systems and is the most common among indies.

{% hint style="warning" %}
There is no way to perform end-to-end testing of the purchase process using the Client API only.
{% endhint %}

This is not a problem and we will show why shortly\
\
As to why this is true its down to two major factors imposed by Valve.

1. Steam Inventory Items will not display in Steam Client until your game is launched. Thus you cant add them to a cart or even view them in Steam Client's inventory window
2. Using only the Client API you never "complete" a transaction you simply load the user's cart and that is the end of your game's involvement. Your now thinking ... how do I know what they purchased ... more on that in a moment.

The following topics in the FAQ should answer all other points

### How do I test StartPurchase

First you define your items and configure your store, this article tells you how to set it up and provides troublshooting instructions

{% embed url="https://partner.steamgames.com/doc/features/inventory/itemstore" %}

Once you have items suitable for the store the only thing you game logic needs to do is call [StartPurchase](../../../objects/item-definition.md#start-purchase) on that item to start a purchase on a single item ... or to gather up an array of items and quantities you want to Start Purchase on and [use the API](../../../api/inventory.client.md#startpurchase) to load up the cart with multiple items.

In either case these methods cant be testing until your game is released **BUT** you don't need to "unit" test them as there is nothing here that you can effect one way or the other. If your item shows up in the store and the user's account is not blocked then this will load the items into the cart and open the Overlay. Your game logic cant do anything here it is out of your hands and not for you to test.

The next logical question related to this is "How do I know what was purchased" ... see the question below for that.

### Detecting what was purchased

First understand that your game cannot know ahead of time what if anything was or is being purchased so the question isn't'

"How do I know what was purchased?"&#x20;

the question should be "How do I detect changes to the player's inventory?"

Remember a lot of things can change the player's inventory most of those things are started and completed outside of your game and don't require your game to even be running. So you need to detect when changes occur in general and not assume its related to some action taken in game such as a purchase.

In short when your game loses and regains focus you will probably want to refresh [all Items](../../../api/inventory.client.md#getallitems). This will cause the system to iterate over the user's whole inventory and if any changes where detected it will raise the [EventChanged](../../../objects/steam-settings/game-client/inventory-settings.md#eventchanged) on the inventory settings.

you can register a listener on the EventChanged from code such as

```csharp
SteamSettings.Client.inventory.EventChanged.AddListener(HandleChange);
```

or you can use the [Inventory Manager](../../../components/inventory-manager.md) to expose the event to the Unity inspector and add a handler to it as you would any other Unity event.

### Testing Inventory Change

So you have set up your inventory items, your going to use full Client API so you cant simulate an end-to-end purchase. Your asking your self ... How do I test my game logic to make sure its handling inventory change correctly?

Use the [Steamworks Inspector](../../debugging-steam-api.md#inventory) and click the "Grant" button beside any of the items, this will cause it to grant you an item which will raise the [EventChanged](../../../objects/steam-settings/game-client/inventory-settings.md) ... you can now observe your game logic and insure its performing as you expected.
