# Inventory

Steam Inventory lets you define items that will be held in the user's Steam Inventory. These items can be made tradable between players, marketable on the community marketplace, made available for sale in the Steam store or your game and can be defined with probability tables and exchange recipes enabling crafting, loot boxes and more.

Steam Inventory is by far the largest, most capable and most complex feature of Steamworks. This article will introduce the general concepts of the system, as the system can be used in many ways for many purposes. Quick start and how-to guides will be separated.

<details>

<summary>Required Reading - <mark style="color:green;">Please don't just skip this; it is important.</mark></summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/features/inventory](https://partner.steamgames.com/doc/features/inventory)
* Schema Documentation\
  [https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

### Items

[https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

This is the most basic unit/object in Steam's Inventory system. An item is a defined concept with a unique ID, name, description and a range of additional metadata depending on the type of item it is and how it can be used. For example, an item can have a "price" which makes it available on the Steam Store, it can also have an "exchange" defined allowing it to be crafted by consuming a given set of other items.

### Bundles

[https://partner.steamgames.com/doc/features/inventory/schema#SpecifyBundles](https://partner.steamgames.com/doc/features/inventory/schema#SpecifyBundles)

This represents a set of items and quantities and when instantiated, unpacks into the collection of items.

### Item Generators

[https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

This is a set of rules that will result in the production of an item. There are various types of generators; the most commonly used would be the PlayTimeGenerator which can be invoked to generate items for a player based on the amount of time the player has played the game.

### Tags

[https://partner.steamgames.com/doc/features/inventory/itemtags](https://partner.steamgames.com/doc/features/inventory/itemtags)

A somewhat advanced feature, tags allow you to mark up an item instance with additional data. For example, your Iron Sword item could have a "Quality" tag with values such as "Quality:Common" or "Quality:Rare"

### Tools

[https://partner.steamgames.com/doc/features/inventory/tools](https://partner.steamgames.com/doc/features/inventory/tools)

Tools are related to tags and allow you to create items that can modify other items, such as changing the tags on an item

### Item Store

[https://partner.steamgames.com/doc/features/inventory/itemstore](https://partner.steamgames.com/doc/features/inventory/itemstore)

Your items can be sold to your players via the item store. This requires the items to have a price or price category and is an optional feature.

### Steam Community Market

[https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

Items can be made marketable by players, which allows players to buy and sell items amongst themselves and results in a small cut of proceeds being relayed to you as the developer. See the `marketable` field on the Schema definition page.

### Steam Trading

[https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

Items can be made tradeable by players, which allows players to trade with each other over the Steam Inventory screen (outside your game). See the `tradable` field on the Schema definition page.

</details>

## What Can It Do?

**Crafting**\
The Steam Inventory system supports an exchange concept where you define a recipe—a collection of items and their quantities—that can be traded for a specific item. While this feature can be used for loot boxes and similar systems, its most user-friendly application is as a crafting system. Players collect reagents (items) and exchange them for gear such as a shield or sword made from iron and leather.

**Microtransactions (MTX)**\
Steam Inventory serves as the framework for defining items available for purchase through the Steam store or your storefront, with management handled by Steam.

**Player Economy**\
Create items that players can securely trade both in and out of the game; these items can also be optionally listed on the Community Marketplace for player-to-player sales.

**In-App Purchase (IAP)**\
Define items that can be purchased in-game, and set up exchange recipes that allow players to buy items using in-game currency through your shop.

**Item Collection and Progression**\
Securely define items, reagents, crafting recipes, drop rates, and probability tables that drive item collection and progression within your game.

**In-Game Economy**\
Manage items, reagents, recipes, drop rates, and loot tables that power your in-game economy. Items managed by Steam Inventory do not have to be available for sale, trade, or community marketing; you can keep them hidden and control every aspect of their distribution, consumption, and use. This system offers a secure method for managing client interactions with items, including generators, drops, and exchanges.

***

## Use

Regardless of how you use the Steam Inventory system, follow these simple guidelines when managing items in your game.

### What Is an Item

An item is simply an integer representing the unique ID of an item type. Each ID is linked to an Item Definition that describes the item's name, price, and other properties. Typically, you only need to know the quantity of each item type a user owns (for example, how many of item type 42 does the user have) and, in a store context, the local price of that item.

### Inventory Snapshot

Items exist outside your game logic and can be affected by various systems, including Steam. Therefore, your game must query the inventory state to determine what items the user owns at any given moment. This snapshot represents the current state, which may change without your game’s knowledge. Valve and Heathen recommend refreshing your view of the inventory just before any critical operation, such as opening an inventory screen or entering a game session where items will be used. Heathen provides tools for easily requesting and inspecting item quantities, tags, and overall state.

### Using Items

User items are presented as a collection of "item details"; each detail represents a stack of a single item type. For example, a user might have 10 stacks of gold, each with a different quantity. Although rare, a stack can have a quantity of 0. Most operations—such as exchanging or consuming items—work with specific item details, each having a unique identifier. Heathen's tools simplify handling these details and building lists for exchanges and consumption, so you usually do not need to sort items manually.

### Exchanging

Exchanging, also known as crafting, involves trading one or more items for a different item. The result is always a single item, which can be a bundle, generator, or any nested type. Examples include:\
• Exchanging 1 chest for a bundle (which might contain multiple items, a generator, or other bundles);\
• Crafting a sword by trading 2 iron and 10 gold for an iron sword;\
• Buying a chest by exchanging 100 gold for 1 chest, which can later be opened to yield a bundle.

### Consuming

Consuming items means deleting them, which applies to consumables like food, boosts, or potions, but can be used to remove any item. Use with caution.

***

## Examples

### Item Definitions

To create your item definitions, you do this in JSON and upload them to your Steamworks developer portal. In the above sections, we outlined the various things you can do and the [Schema](https://partner.steamgames.com/doc/features/inventory/schema) link at the top guides you to Valve's documentation on creating that JSON.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Once you have created your Steam Inventory Items in the Steam Developer Portal, you can access them in your project via code, through the Item Data struct or the Inventory API. You can also access your item definitions via Scriptable Objects using the Steam Settings object.&#x20;

In all cases, using your Item Definition, you will be able to

* Determine if the user owns this item and how many they own
* Be able to start a purchase of this item
* Be able to combine this item
* Be able to use this item in an exchange recipe
* Be able to exchange other items (recipes) for this item
* Be able to read the item's price, name and other attributes if set

{% hint style="info" %}
Heathen's system will attempt to track changes to the items that Steam notifies the game of, and in many cases, this can keep the item state up to date through gameplay. \
\
However:\
It's important to remember that changes can occur to the items from outside your game's view. As such, anytime you need to "know" with a level of certainty how many or what items the player owns, you should perform a Get All Items
{% endhint %}

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

To import your Steam Inventory Item Definition into your project, you need to start your game in the Editor so that the Steam API can initialise. Then, open your Steam Settings in the inspector and click the Import option under the Inventory section.

Once complete, you can now use the Generate Wrapper, and your Unity Project will have access to your Steam Inventory Items.

You can use the Inventory Item component to access and work with your items.

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

## C\#

We have created simple structs in C# that let you do everything you might want to do with an item and all you need is that item's ID.&#x20;

```csharp
// Assuming you have an item whose ID is 100, this is now that item
ItemData myItem = 100;
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
This is optional; you do not have to pre-register your item definitions, but if you prefer to work with references, this can be a handy approach, allowing our system to manage inventory query results and load them into your predefined references.

### Game Instance & Data Assets

You can define your Inventory Items as Inventory Item Data Assets

<figure><img src="../.gitbook/assets/image (306).png" alt=""><figcaption></figcaption></figure>

Once created, you can set the Item Definition ID ... this is the ID you created when you uploaded your Item Definition JSON to the  Steamworks Developer Portal

<figure><img src="../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>

With the inventory, Item is defined as a Data Asset you can then reference the item in you Steam Game Settings blueprint.

<figure><img src="../.gitbook/assets/image (308).png" alt=""><figcaption></figcaption></figure>

Doing so allows our systems to update the Inventory Item Details of this data asset for you any time you use the "Simple" versions of inventory requests, such as Get All Items - Task

<figure><img src="../.gitbook/assets/image (326).png" alt=""><figcaption></figcaption></figure>

It also allows you to work with this item type in a context-sensitive manner ... for example, you could create a variable Inventory Item Data Asset in a Blueprint and set your item as its default value.

<figure><img src="../.gitbook/assets/image (310).png" alt=""><figcaption></figcaption></figure>

You can now use the Iron Ingot variable to work with this item type however you choose.

<figure><img src="../.gitbook/assets/image (311).png" alt=""><figcaption></figcaption></figure>



### Global Events

Steamworks has a number of global events that we have exposed to you as Blueprint bindable events from the Steam Game Instance along with giving you a simple "Get Steam Game Instance" node to easily access your instance.

<figure><img src="../.gitbook/assets/image (312).png" alt=""><figcaption></figcaption></figure>

The following are just a few of the most common use cases or needs regarding Steam Inventory. If you check the articles below this article, you will find more specific cases such as Crafing Systems, Microtransactions and Promo Items
{% endtab %}

{% tab title="Steamworks.NET" %}
Not Applicable
{% endtab %}
{% endtabs %}

### Get All Items

For efficiency, Steamworks Inventory uses a local cache. The SDK keeps the player's inventory data locally, so actions like reading an item's quantity are effectively instant. Get All Items asks Steam.exe to refresh this cache; it's recommended to call this just before any in-game action where you need an accurate view, and values may have changed from outside the game, such as opening the inventory UI.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can call Get All Items from any Inventory Item component.

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

## C\#

This can be done using the static Update function on ItemData.

```csharp
// Using ItemData
ItemData.Update(HandleInventoryUpdate);
```

Or by using the Inventory.Client static class

```csharp
// Using API Extensions
Inventory.Client.GetAllItems(HandleInventoryUpdate);
```

In either case, the handler will look like such

```csharp
void HandleInventoryUpdate(InventoryResult response)
{
    // response.result is the EResult indicating if this is good or not
    // response.items is an array of ItemDetail describing all details found
    // response.timestamp is when this was returned originally
}
```

Once the handler has returned, you can then use ItemData for specific items to check quantities and perform similar actions.

```csharp
ItemData myItem = 100;
Debug.Log($"The player has {myItem.GetTotalQuantity()} of item ID 100");
```

You can do something similar using the Inventory.Client

```csharp
long quantity = Inventory.Client.ItemTotalQuantity(100);
Debug.Log($"The player has {quantity} of item ID 100");
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
This is how you "refresh" your view of the player's inventory. We provide 3 variations of this feature in Blueprints, with the Task variant being the most commonly used.

<figure><img src="../.gitbook/assets/image (323).png" alt=""><figcaption></figcaption></figure>

As you can see, the Get All Items - Task is an asynchronous node that will run the Completed pin when Steam responds with the results. The Result point is the EResult enumerator describing the status of the call, and Items will be the items found, if any.

If you prefer to work with the callbacks yourself self you can use our Get All Items - Simple node, which will invoke an event when the result is ready and works more similarly to the native Steamworks SDK, but does package the results for you, saving you from manually managing the result handle.

{% hint style="info" %}
When you're working with Inventory Item Data Assets, you should either always use the Simple variation or you need to manually clear and update details on the Steam Game Instance
{% endhint %}

<figure><img src="../.gitbook/assets/image (313).png" alt=""><figcaption></figcaption></figure>

You optionally pass in an array of strings representing the custom properties you would like the system to read from the resulting items. When the callback is executed it will define its result state and if not a failed condition it will include an array of the Item Details with Properties it found. You can think of each of these as a "stack" of 0 to many of a given item type.

The Definition ID of the item detail tells you what type of item it is, and the instance ID can be used with other functions, such as consume or exchange.

#### Native Style

In the above example, we used the "Simple" version of the Get All Items, which takes in a delegate that will be called when the process completes, letting our internal systems manage the callback for you. You can optionally bind to a global event listening for all "Inventory Result Ready" calls and compare the result ready "handle" with the handle provided by the native "Get All Items"

<figure><img src="../.gitbook/assets/image (314).png" alt=""><figcaption><p>Here we request Steam to fetch all items, Steam will give us a result handle identifying this particular request</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (315).png" alt=""><figcaption><p>Here we are listening on the global event for Inventory Result Ready when we get that we compare it to our handle to see if its from our request.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (316).png" alt=""><figcaption><p>Assuming it is from our request we can ask Steam to read us back the results based on that result handle</p></figcaption></figure>

As you can see, our "Simple" variant greatly simplifies the process and handles the internals for you.

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
First, you will need to register a callback to handle the response from Steam

```csharp
m_ResultReady_t = Callback<SteamInventoryResultReady_t>.Create(HandleInventoryResults);
```

The handler for this will take the form of

```csharp
void HandleInventoryResults(SteamInventoryResultReady_t results)
{
}
```

The actual call to Get All Items is simpler

```csharp
SteamInventory.GetAllItems(out SteamInventoryResult_t resultHandle);
```

The result handle can then be used in your callback handler to match the response to the request.

```csharp
void HandleInventoryResults(SteamInventoryResultReady_t results)
{
    //Compare the result ready handle to the anticipated handle
    if(results.m_handle == resultHandle)
    {
        //Assuming it is an expected result, you can read data from it
    }
}
```

Note that this same callback is used for all requests, so this is invoked anytime an inventory query result is ready. It is up to you to track the result, handle and then handle each result ready response accordingly.
{% endtab %}
{% endtabs %}

### Check Quantity

How do you know if the user owns any of a given item, and if so, how many?

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add an Inventory Item component&#x20;

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

Then add a quantities field

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

This can be used to display the quantity of this item the player owns

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

## C\#

Using the Item Data structure

```csharp
//Assuming your item
ItemData myItem = 100;

//Then you can read the quantity
Debug.Log($"The player has {myItem.GetTotalQuantity()} of item ID 100");
```

Or you can use the API

```csharp
long quantity = Inventory.Client.ItemTotalQuantity(100);
Debug.Log($"The player has {quantity} of item ID 100");
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

If you are using SteamInventoryData assets and letting our system manage that for you, then you can read the quantity from your reference easily at any time after Getting All Items or a similar query.

<figure><img src="../.gitbook/assets/image (324).png" alt=""><figcaption></figcaption></figure>

If you choose not to use Inventory Item Data Asset, then you will have to sum the total of the details returned in the SteamInventoryResults, which can be cumbersome

<figure><img src="../.gitbook/assets/image (325).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Add Promo Item

This lets you "give" users an item; in general, Steam Inventory doesn't allow you to just give users items when you want, but promotional items can be. If you read the above documentation, you can learn more about creating items that can be given to users, just once or multiple times.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add an Inventory Item component&#x20;

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

You can use the Add Promo to add this item as a promotional item to the player's inventory. This assumes you have properly configured this item as a promotional item in the Steamworks Developer Portal.

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Then add a Events settings

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

You can use these events:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

To handle the results of the Add Promo function.

### On Add Promo Rejected

This is raised in response to:

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

It indicates a direct rejection of the request by Steam. No further action will be taken.

### On Add Promo Failed

This is raised in response to:

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

It occurs when the request was accepted but then failed in processing on Steam. The EResult value it provides will indicate why it failed.

### On Add Promo Complete

This is raised in response to:

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

It occurs when the request was accepted and completed by Steam. The ItemDetrail array it provides is the items effected by the process if any. In generally we would recomend you Get All after any such change to fully refresh the internal view of the inventory.

## C\#

```csharp
// Assuming 
ItemData myItem = 100;
// or
ItemDefinitionObject myItem; // Drag and drop in the inspector

//Then you can request the item to be added. Note that it will only be added
//If the rules you defined on the item in the Steamworks Developer Portal
//Resolve for this user
myItem.AddPromoItem(HandleResult);
```

Or you can use the API

```csharp
Inventory.Client.AddPromoItem(100, HandleResult);
```

The callback delegate takes the form of&#x20;

```csharp
void HandleResult(InventoryResult response)
{
    // response.result is the EResult indicating if this is good or not
    // response.items is an array of ItemDetail describing all details found
    // response.timestamp is when this was returned originally
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

The most commonly used approach is to use the Add Promo Item - Task node.&#x20;

<figure><img src="../.gitbook/assets/image (327).png" alt=""><figcaption></figcaption></figure>

This is an asynchronous node whose completed pin will be run when the process is complete and will provide you with the results, if any.

If you are using Inventory Item Data Assets, you can do this from the data asset as well.

<figure><img src="../.gitbook/assets/image (328).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamwork.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Get Price

If your item has a valid price or price category set, you can request the current price and get the data for the local user. This is useful when creating in-game cash shops.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add an Inventory Item component&#x20;

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

Add Current and or Base price fields

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Note that this will add the Events settings as well

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

### Current Prices

Current price the price the player will pay right now should they purchase, it accounts for any sales or temporary discounts.

Attach a TMP Pro uGUI text and it will be populated with the player localized value of the item if any. for example an American mith see $1.50 while a German might see €1,00

### Base Price

The base price is the unmodified price of the item, e.g. before any sales or temporary discounts are applied.

Attach a TMP Pro uGUI text and it will be populated with the player localized value of the item if any. for example an American mith see $1.50 while a German might see €1,00

## C\#

```csharp
// Assuming 
ItemData myItem = 100;
// or
ItemDefinitionObject myItem; // Drag and drop in the inspector

// Before you work with prices, be sure to request the prices
// This is normally done for you on initialisation
// but be sure
ItemData.RequestPrices((result, ioError) =>
{
    // if result.m_result is okay and ioError is false, all is well
});

// get the current and base price (base price is before sales/promos)
myItem.GetPrice(out ulong currentPrice, out ulong basePrice);

// get the current price as a human-friendly string ... this assumes
// the currency is based on 100 (USD, GBP, Euro, etc.)
string price = myItem.CurrentPriceString();
// and the same for base price
string basePrice = myItem.BasePriceString();

// Do you just need the currency symbol? .. e.g. $, €, £, etc
string symbol = ItemData.CurrencySymbol;
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Before you do anything with prices, you will want to request prices. This will update the cash with the items' prices, and it will report the currency code and symbol used by this user, which will be important for displaying prices later.

<figure><img src="../.gitbook/assets/image (330).png" alt=""><figcaption></figcaption></figure>

If you are using Inventory Item Data Assets, you can read this from the asset itself

<figure><img src="../.gitbook/assets/image (329).png" alt=""><figcaption></figcaption></figure>

You will notice that the values are whole numbers; for currencies that use decimal values, simply divide by 100. For example, a value of 99 where the user's currency is Euro would be €0.99

You can also request an array of all the items that have prices. This can simplify building out a store page.

<figure><img src="../.gitbook/assets/image (318).png" alt=""><figcaption><p>Get all item definitions that have a defined price valid for this user</p></figcaption></figure>

You can then read the current and base price for this user; note that the current and base price are int64 (long) values. It is the base 100 value. e.g. $1.99 would be returned as 199.

<figure><img src="../.gitbook/assets/image (319).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Start Purchase

You can add one or more items to a user's Steam shopping cart directly from your game by calling **Start Purchase**. If the provided inputs are valid, such as a valid item, price, and availability for the user, the Steam overlay will open and display the item in the shopping cart.

Starting the purchase does not initiate the payment process; it simply adds the item to the cart. The user can then modify or complete the purchase at their discretion. If they choose to proceed, **MTX Txn Authorisation Response** events will be triggered within the game.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add an Inventory Item component&#x20;

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

Then add a Events settings

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

With the events added&#x20;

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

You can use the following events to handle the results of the request:

### On Purchase Started

This is raised in response to:

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

It does not indicate that the purcahse is complete only that the item was added to the user's cart in the Steam client. This will have also opened the overlay to the user's cart where they can choose to complete or cancel or modify the purchase.

### On Purchase Start Failed

This is raised in response to:

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

It indicates the requested item cannot be set to the user's cart. Generally this is because the item is not available to the user, or the item is simply not available at all. you can check what Items are valid for purcahse by previewing the item store in your Steamworks Developer portal. If the item doesn't show in that preview then it is not elegable for purcahse. Usually becuase you have not properly defined a price for it or you have explicitly removed it form purcahse.

### On Order Authorized

This is raised when the user authorizes any purchase involving the game, it will provide you with the order id of that order. Note the Start Purchase arguments will tell you the order ID the start purcahse request was attached to so you can use that to match a completed order to a started purcahse if required.

### On Order Not Authorized

This is raised when the user cancels any purchase order involved the game.

## C\#

```csharp
// Assuming 
ItemData myItem = 100;
// or
ItemDefinitionObject myItem; // Drag and drop in the inspector

// Assuming myItem is valid for purchase (has a price, is not blocked or hidden)
// How many to buy?
uint count = 1;
myItem.StartPurcahse(count, (result, ioError) =>
{
    if(!ioError && result.m_result == EResult.k_EResultOK)
    {
        ulong OrderId = result.m_ulOrderID;
        ulong TransactionId = result.m_ulTransID;
    }
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

For items that have a valid price and are enabled for purchase in their item definition, you can form the gate "start purchase" ... what this does is simply load the items into the Steam shopping cart and give you an Order and Transaction ID that represents that as of yet incomplete transaction.

<figure><img src="../.gitbook/assets/image (320).png" alt=""><figcaption></figcaption></figure>

As noted, this "starts" the process, but does not mean the transaction is completed. You can listen to the Micro Transaction Authorization Response event to know when a transaction is completed and check it against the Order ID provided in the Start Purchase process.

<figure><img src="../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>

Note that a transaction can fail or be cancelled... so it's the "Authorized = True" that indicates this order is complete. Also, be aware that the user may have changed the state of the shopping cart before completing the transaction, so items may have been added or removed. It would be advisable to check the state of the inventory again or to listen to the Inventory Results Ready event and listen for changes to the player's inventory

<figure><img src="../.gitbook/assets/image (322).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
Comming Soon
{% endtab %}
{% endtabs %}

### Exchange

Exchange allows you to securely exchange 1 or more items for another item. This can be used for several in-game features, such as

#### In-Game Store

Allow your players to earn in-game currency and securely exchange it for items. You can also implement premium currency, where players "purchase" the currency. However, be cautious with this form of monetisation, as it often leads to negative outcomes.

#### Lootbox

This is where you have a single item that gets "opened" to reveal 1 or more items. This is effectively simply exchanging the "lootbox" for an item generator or bundle.

#### Crafting

This is where your player finds, earns, or purchases reagents that can then be "forged", aka "exchanged", for something else.&#x20;

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add an Inventory Item component&#x20;

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

Then add a Events settings

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

With the Exchange and Events components added, you can define the recipe for the exchange ... note this must match a recipe defined in your Item Definition that is uploaded to Steamworks Developer Portal.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

You can use the following events to drive your UI and respond to exchange results.

### On Can Exchange Change

This raises any time your inventory changes or if you call:

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

It carries a bool so you can use it to toggle UI elements on and off, such as toggling a "Craft" or "Buy" button based on whether or not the player has the necessary items for this exchange.

### On Exchange Rejected

This is raised in response to:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

If the request to exchange was rejected, this usually indicates that the required items could not be secured for the exchange. If you feel this is in error, you should generally call Get All,

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

This will refresh the internal view of all inventory items, then attempt the exchange again, assuming you do still have the required reagents.

### On Exchange Failed

This is raised in response to:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

If the request to exchange is responded to with a failure state, the EResult it provides tells you what that failure was.

### On Exchange Completed

This is raised in response to:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

If the request was a success, the ItemDetails it provides indicate what, if any, items changed as a result of this exchange request. It is generally advisable to call GetAll after a successful exchange to refresh the internal state of the inventory.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## C\#

1st, you will need to get the items you wish to exchange, for example, if you wish to exchange 100 iron bars for 1 sword, then you first need to get the specific instances of those 100 iron bars.

The second step is to exchange those iron bars for the sword

```csharp
ItemData ironBar = 100;    // Assume Item ID 100 = Iron Bar
ItemData ironSword = 200;  // Assume Item ID 200 = Iron Sword
if(ironBar.GetExchangeEntry(100, out EchangeEntry[] entries))
{
    // We have 100 iron bars found
    ironSword.Exchange(entries, (result, error) =>
    {
        if(!error)
        {
            // The exchange completed, the results define what was added
            Debug.Log("Complete");
        }
    });
}
else
{
    Debug.Log("Not enough iron");
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

1st, you would need to get the instance ID of the stacks you will exchange from. For example, the Toolkit let us assume we want to exchange 50 iron bars for an iron sword. Our first step is to find the Instance ID of a stack of Iron Bars that has 50 or more.&#x20;

The easiest way to do this is to define your Items as Item Data objects in your project, so create two new Data Assets in your project of type Inventory Data Asset.

<figure><img src="../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

This would be Iron Bar and Iron Sword. You would set the ID for each. In our example, Toolkit, we will assume the ID is 100 for the Iron Bar and 200 for the Iron Sword.

<figure><img src="../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

Now, in any Blueprint where you want to work with Iron Bar or Iron Sword, simply create a variable of type Inventory Item Data, save, compile and set the default to your desired object.

<figure><img src="../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

We can now use these data objects for our exchange.,

<figure><img src="../.gitbook/assets/image (165).png" alt=""><figcaption></figcaption></figure>

Alternatively, we can use the Task node if we don't want to bother with a custom event.

<figure><img src="../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Steamwroks.NET" %}



{% endtab %}
{% endtabs %}

### Serialize Inventory

**Serialise Inventory** is used when an authenticated user needs to prove ownership of specific inventory items. This feature allows a user to generate a serialised representation of their inventory—either the full inventory or a selected subset—which can be shared as proof of ownership.

For example, in a card collection game, a player may need to prove to their opponent that they own all the cards in their deck. By serialising the relevant cards, the player can present a verifiable snapshot of those items, authenticated by the Steam backend.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not Applicable

## C\#

```csharp
// Get the serialized data for the player's enter inventory
Inventory.Client.SerializeAllItemResults(data =>
{
    // Send data to the player or server who needs it
});

// Get the serialized data for a specific item or items
ItemData item = 100;
var details = item.GetDetails();
var instance = new SteamItemInstanceID_t[details.Count];
for(int i = 0; i < details.Count; i++)
    instance[i] = details[i].itemDetails.m_itemId;

Inventory.Client.SerializeItemResultsByID(instance, data =>
{
    // Send data to the player or server who needs it
});

// On the player or server that needed the data
Inventory.Client.DeserializeResult(whoSentIt, data, response =>
{
    if(response.result == EResult.k_EResultOK)
    {
        // whoSentIt defently owns these items
        response.items // <--
    }
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

This is used to serialise a result handle, so you will first need to "get" the inventory you wish to serialise the result for. Typically, you would be "getting" a specific set of inventory items so you can send that to another user or server to validate your ownership of them ... or you can "Get All"

<figure><img src="../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure>

The "Result Handle" is what you will pass into the Serialise Result; the output is an array of bytes that can be sent to whoever it is that you want to send this snapshot to.

<figure><img src="../.gitbook/assets/image (378).png" alt=""><figcaption></figcaption></figure>

With the result sent, the receiver of that data will use Deserialise Result to convert that back to inventory item data, thus giving them a clear view of what you do own in terms of Steam Inventory items.

<figure><img src="../.gitbook/assets/image (380).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Steamwroks.NET" %}

{% endtab %}
{% endtabs %}

### Consume / Delete Items

You should rarely, if ever, need to do this; this cannot be reversed once done.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add an Inventory Item component&#x20;

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

Then add a Events settings

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

You can use the following events:

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

To respond to the results of the request

### On Consume Request Rejected

This is raised in response to (ONE) of these:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

And indicates that the request was rejected, for example, if the player does not have any of those items.

### On Consume Request Failed

This is raised in response to (ONE) of these:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

And indicates that the request failed processing on Steam.

### On Consume Request Complete

This is raised in response to (ONE) of these:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

And indicates that the request was completed and indicates the items effected if any.

## C\#

```csharp
// Assuming 
ItemData myItem = 100;
// or
ItemDefinitionObject myItem; // Drag and drop in the inspector

// Then to consume 1 
myItem.Consume(result =>
{
    // result is an InventoryResult and can be used to see what was done
});

// To consume a defined number ...
// Note this may construct multiple consume orders if the requested number is 
// split across various stacks of items
myItem.Cosnume(42, result =>
{
    // result is an InventoryResult and can be used to see what was done
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

To consume an item, you need the instance ID of the item you wish to consume. You can then simply call Consume Item, providing that instance ID and the quantity you wish to consume from it. As with most functions, you will find 3 variants of the node, all do the same thing, they simply handle the result in the 3 different options available to you in Unreal.

<figure><img src="../.gitbook/assets/image (377).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}
