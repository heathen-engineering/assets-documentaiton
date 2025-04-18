---
description: Hands down the largest and most complex of all Steam features
---

# 📦 Inventory

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Steam Inventory lets you define items that will be held in the user's Steam Inventory. These items can be made tradable between players, marketable on the community marketplace, made available for sale in the Steam store or in your game and can be define with probaiblity tables and exchange recipies enabling crafting, loot boxes and more.

Steam Inventory is by and far the largest, most capable and most complex feature of Steamworks. This article will introduce the general concepts of the system, as the system can be used in many ways for many purposes quick start and how to guides will be separated out.

{% hint style="warning" %}
You cannot test Steam Inventory features with App ID 480 aka Spacewars.

\
To test Steam Inventory features including but not limited to microtransactions, crafting, player inventory, etc. you will need to register for your app ID and configure your own Steam Inventory Items.\
\
As a result of this limitation from Valve, the sample scenes for Inventory cannot be used with App 480 in any functional form.
{% endhint %}

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/features/inventory](https://partner.steamgames.com/doc/features/inventory)
* Schema Documentation\
  [https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

</details>

## What can it do?

### [Crafting](../../../../steam/inventory/crafting-system.md)

The Steam Inventory system has a concept of "exchange" wherein you can define a "recipe" being a collection of items and quantities that can be "exchanged" to receive a specific item.

The Exchange feature can be used to create loot boxes and other systems but far less predatory is the use as a crafting system. That is the player can collect reagents which you have defined as items and exchange them for specific items such as iron and leather to be exchanged for a shield or sword.

### [Microtransaction (MTX)](../../../../steam/inventory/microtransactions.md)

Steam Inventory is the interface and framework you would use to define items for purchase either through the Steam store or through your store to be managed by Steam.

### Player Economy

Steam Inventory is how you create items that can be traded between players securely both in and out of the game and can optionally be put on the "Community Marketplace" for sale by players to players.

### [In-App Purchase (IAP)](../../../../steam/inventory/microtransactions.md)

Steam Inventory is the framework you would use to define the items that can be purchased in-game and the exchange "recipes" that define how a player can "purchase" an item in-game for an in-game item e.g. in-game currency, in-game shop, etc.

### Item Collection / Progression

Steam Inventory is the framework you would use to define the items, reagents, crafting "recipes", drop rates and probability tables that drive item collection and item progression game loops in a secure manner

### In-game Economy

Steam Inventory is the framework you would use to define the items, reagents, recipes, drop rates, loot tables, etc. that drive these systems.&#x20;

No Steam Inventory items do not have to be available for sale, trade or community marketing you can hide them in inventory and control every aspect of how they are distributed, consumed and used. It is simply a secure way of defining the client's interaction with the items, the items themselves and related features of those items e.g. generators, drops, exchanges, etc.

## Required Reading

Steam Inventory can be used for consumables, craftables, player economy (marketplace and trading) and microtransactions. The system is concerned first and foremost with security and this can make it a more cumbersome feature than you need if you're not taking advantage of either the player economy or MTX aspects of the system.

{% hint style="warning" %}
You can use Steam Inventory with no backend / trusted server at all, leveraging Valve's store and rules defined in the developer portal. This however does have restrictions such as not being able to "grant" a specific item at a specific time to a client. These restrictions are to ensure security.

In short, a "client" can never be trusted so it can't do anything that cannot be validated by Valve. As a result, items can only be generated for users via the PlayTimeGenerator feature, Promo feature or as part of a Steam Store or Steam Marketplace purchase (or trade).
{% endhint %}

{% hint style="info" %}
The following is taken directly from Valve's documentation. you should read Valve's documentation.

[https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)
{% endhint %}

### Items

This is the most basic unit/object in Steam's Inventory system. An item is a defined concept with a unique ID, name, description and a range of additional metadata depending on the type of item it is and how it can be used. For example, an item can have a "price" which makes it available on the Steam Store, it can also have an "exchange" defined allowing it to be crafted by consuming a given set of other items.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

### Bundles

This represents a set of items and quantities and when instantiated unpacks into the collection of items.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema#SpecifyBundles" %}

### Item Generators

This is a set of rules that will result in the production of an item. There are various types of generators, the most commonly used would be the PlayTimeGenerator which can be invoked to generate items for a player based on the amount of time the player has played the game.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

### Tags

A somewhat advanced feature, tags allow you to markup an item instance with additional data. For example, your Iron Sword item could have a "Quality" tag with values such as "Quality:Common" or "Quality:Rare"

{% embed url="https://partner.steamgames.com/doc/features/inventory/itemtags" %}

### Tools

Tools are related to tags and allow you to create items that can modify other items, such as changing the tags on an item

{% embed url="https://partner.steamgames.com/doc/features/inventory/tools" %}

### Item Store

Your items can be sold to your players via the item store. This requires the items to have a price or price category and is an optional feature.

{% embed url="https://partner.steamgames.com/doc/features/inventory/itemstore" %}

### Steam Community Market

Items can be made marketable by players, this allows players to buy and sell items amongst themselves and results in a small cut of proceeds being relayed to you as the developer. See the `marketable` field on the Schema definition page.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

### Steam Trading

Items can be made tradeable by players, this allows players to trade with each other over the Steam Inventory screen (outside your game). See the `tradable` field on the Schema definition page.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

## Use

No matter your intended use of the Steam Inventory system you will need to follow some simple guidelines when working with items in the game.&#x20;

### What is an Item

In reality, an item is just an int ... i.e. it is a number\
The number is the unique ID of that item type, it's associated with an Item Definition which describes the type of item, its name, price, etc.&#x20;

When using items in the game you generally only need to know how many of what item types the user owns. e.g. how many of item type 42 does the user own?

When using items in a store you only need to know the price of the item, e.g. what is the local user's price for item 42?

### Inventory Snapshot

First, you need to understand that the items do not "live" in your game logic and can be affected by many different systems including Steam itself without your game being aware of or even involved in the transaction. As such your game will need to query the state of the inventory to understand what items the user owns at the time of that query. That view is just that, a view of the items at that time, the item states, quantities, etc. may change over time without your game being aware of it.

The approach Valve (and Heathen) recommends is that you "refresh" your game's view of the items the user owns just before any important use of the items, such as just before opening an inventory screen, or just before entering a game session where 1 or more items will be used. Heathen provides you with simple and easy-to-use tools for requesting all items and inspecting the quantities, tags and general state of each item found.

### Using Items

Your view of the user's items will be a collection of "item details" Each detail represents a stack of 0 to many items in the user's inventory. Each stack will have just 1 item type.

For example:\
I could have 10 stacks of gold each with different quantities of gold in each of the stacks. While rare it is technically possible for a stack to have 0 quantity so you can't assume a stack means 1 or more.

Most of the operations you will do on items such as "Exchanging", "Consuming", etc. will work with specific item details. Each Item Detail has a unique identifier for this purpose.

Heathen's tools simplify working with item details and building out lists of details for exchanges and consumption so you don't generally need to deal with sorting items yourself.

#### Exchanging

Exchanging aka Crafting, is the process of trading 1 or more items for some different item. The result of an exchange is always 1 item, that 1 item can be of type bundle or even generator or any nested type thereof. Examples follow

Opening a Chest or Box\
Exchange 1 Chest for a bundle, the bundle could contain more than 1 item or generator or other bundles.

Crafting a Sword\
Exchange 2 iron and 10 gold for an Iron Sword

Buying a Chest ... which we can later open\
Exchange 100 gold for 1 Chest ... that we could exchange for a bundle

#### Consuming

You can "consume" items as well, this is simply deleting the item and would be used for consumables like food, boosts, potions, etc.

## F.A.Q

### Generating Items

How do I generate or grant an item to a player at run time?

For testing a developer account can generate any item at runtime by simply calling the [GenerateItem](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-definition.md#generate-item) method on the item definition or the corresponding command on the [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#generateitems).

This however will not work for players

{% hint style="warning" %}
Generate Items can only be used by developers for testing purposes.
{% endhint %}

For security reasons, there is no straightforward way to generate a specific item for the user from the Steam Client API. To give players items you need to do one of the following

* Promo Items\
  You can grant players items as part of a promotion. These are 1-time grants of free items and require the item to be configured as a "promo" item if done correctly you can use [AddPromoItem](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-definition.md#add-promo-item) on the item definition or the corresponding command in the [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#addpromoitem) to grant the item.
* Drop Items\
  You can define play time generators that can be used to grant players items based on client-side rules ... mainly play time and or ownership of specific apps. This method requires you to configure a "Play Time Generator" with the required rules to drop the item and then to call [TriggerDrop](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-definition.md#trigger-drop) on the item or the corresponding [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#triggeritemdrop) call.&#x20;
* Web API\
  You can use the Web API on a trusted web server to perform more direct actions like simply adding an item to a target player's inventory. This requires you to have a trusted web server using a publisher token on the Steam Web API. The Web API is out of scope for Unity assets as it's not part of Unity. You can learn more [here](https://partner.steamgames.com/doc/webapi/IInventoryService).

### In-Game Store

How do you create an in-game store for your items?

In the same way, you create any Unity UI, the visual and UI aspects of your store are wholly up to you. That is you being the developer know what items you have and should create a UI to present those to the player.

As to starting a purchase from your UI, you can use the [Start Purchase](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-definition.md#start-purchase) command on the item definition or the corresponding [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#startpurchase) call.

If you're exchanging an item or group of items for another item e.g. in-game currency for an in-game item. then use the [Exchange](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-definition.md#exchange) feature on the item definition or its corresponding [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#exchangeitems) call.

For more details see the [learning article here](./#item-store).

### Importing Generator Items

You will notice when importing Generator-type items that Valve for some reason chose to hide the bundle aka "items" from the import. As such when importing Generator Items the content of the item will be blanked and you will need to manually redefine its content.

This is a limitation from Valve confirmed with Valve engineers as a deliberate limitation.

> Thanks for the additional context - it helps to see the results you're getting.
>
> I reached out to an engineer who worked on this API for some background. The GetItemDefinitionProperty API intentionally prevents the client from retrieving the bundle property of generator items. If the games you work with need in-game access to that data, they'll need to either include that information in their game builds or create some other service for retrieving it.
>
> Best,&#x20;
>
> Tavish

The above quote is from a Valve support case on this topic. It is not a bug nor a limitation we can effect. If you would like to see this changed you will need to raise it with Valve.

## Examples

{% tabs %}
{% tab title="Toolkit for Unity" %}
Once you have created your Steam Inventory Items in the Steam Developer Portal you can access them in your project via code, through the [Item Data](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-data.md) struct or the [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md). You can also access your item definitions via Scriptable Objects using the Steam Settings object.

In all cases using your Item Definition you will be able to

* Determine if the user owns this item and how many they own
* Be able to start a purchase of this item
* Be able to combine this item
* Be able to use this item in an exchange recipe
* Be able to exchange other items (recipes) for this item
* Be able to read the item's price, name and other attributes if set

{% hint style="info" %}
Heathen's system will attempt to track changes to the items that Steam notifies the game of and in many cases this can keep the item state up to date through gameplay. \
\
However:\
It's important to remember that changes can occur to the items from outside your game's view. As such anytime you need to "know" with a level of certainty how many or what items the player owns you should perform a Get All Items
{% endhint %}

### Scriptable Objects

To import you Steam Inventory Item Definition into your project as Scriptable Objects you need to start your game in Editor so that the Steam API can initialize. Then open your Steam Settings in the inspector and click the Import option under the Inventory section

<figure><img src="../../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

This may take a few seconds to complete but it will import all [item definitions](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-definition.md) and create a Scriptable Object representation for each one stored under the Steam Settings object similar to Stas, Achievements and other Steam artifacts.

### Data Layer

In cases where you prefer to work in purse code or simply wish to avoid reference type objects such as Scriptable Objects, you can use the Data Layer struct [Item Data](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-data.md) to access your Item Definitions. As is always the case with the Data Layer you do not need to initialize or configure objects ahead of time. The Data Layer works on data without reference so you only need to know the uint ID of the item you wish to work with.

### API

The Data Layer as noted above is simply a struct that wraps around the underlying Inventory API. Some programmer-centric developers may be more comfortable working with API endpoints than with structs and so you can access everything you need via the [Inventory.Client](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md) API

### Related Objects

The following are objects and tools in Steamworks Complete that can help you work with Steam Inventory.

#### Inventory API

Learn more in our [Inventory API](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md) documentation.

#### Item Definition

Defines a Steam Inventory Item and provides access to commonly used features as well as the full definition of the item. You can learn more about the creation and use of [Item Definitions](./#item-definitions) in the section above.

#### Item Detail

An object is used to detail an instance of an item in the player's inventory. Learn more [here](../../../../old-toolkit-for-steamworks/unity/objects/classes/item-detail.md).
{% endtab %}

{% tab title="Toolkit for Unreal" %}


### Game Instance & Data Assets

You can define your Inventory Items as Inventory Item Data Assets

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once created you can set the Item Definition ID ... this is the ID you created when you uploaded you Item Definition JSON to Steamworks Developer Portal

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

With the inventory, Item is defined as a Data Asset you can then reference the item in you Steam Game Settings blueprint.

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Doing so allows our systems to update the Inventory Item Details of this data asset for you any time you use the "Simple" versions of inventory requests such as Get All Items - Simple

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

It also allows you to work with this item type in a context-sensitive manner ... for example, you could create a variable Inventory Item Data Asset in a Blueprint and set your item as its default value.

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can now use the Iron Ingot variable to work with this item type however you choose.

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>



### Global Events

Steamworks has a number of global events that we have exposed to you as Blueprint bindable events from the Steam Game Instance along with giving you a simple "Get Steam Game Instance" node to easily access your instance.

<figure><img src="../../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

The following are just a few of the most common use cases or needs regarding Steam Inventory. If you check the articles below this article you will find more specific cases such as [Crafing Systems](../../../../steam/inventory/crafting-system.md), [Microtransacitons](../../../../steam/inventory/microtransactions.md) and [Promo Items](promo-items.md)

### [Get All Items](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/get-all-items.md)

This is how you "refresh" your view of the player's inventory. We provide 2 variations of this feature in Blueprints with the Simple variant being the most commonly used.

{% hint style="info" %}
When your working with Inventory Item Data Assets you should either always use the Simple variation or you need to manually Clear and Update details on the Steam Game Instance
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You optionally pass in an array of strings representing the custom properties you would like the system to read off the resulting items. When the callback is executed it will define its result state and if not a failed condition it will include an array of the [Item Details with Properties](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/types/item-detail-with-properties.md) it found. You can think of each of these as a "stack" of 0 to many of a given item type.

The Definition ID of the item detail tells you what type of item it is and the instance ID can be used with other functions such as consume or exchange.

#### Native Style

In the above example, we used the "Simple" version of the Get All Items, this takes in a delegate that will be called when the process completes letting our internal systems manage the callback for you. You can optionally bind on a global event listening for all "Inventory Result Ready" calls and compare the result ready "handle" with the handle provided by the native "Get All Items"

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Here we request Steam to fetch all items, Steam will give us a result handle identifying this particular request</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Here we are listening on the global event for Inventory Result Ready when we get that we compare it to our handle to see if its from our request.</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Assuming it is from our request we can ask Steam to read us back the results based on that result handle</p></figcaption></figure>

As you can see our "Simple" variant greatly simplifies the process and handles the internals for you.

### [Get Item Price](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/get-item-price.md)

If you are setting up an in-game store or some similar microtransaction system you will likely want to know what the price of the item is for this user.

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>First, you should request Steam to cash the prices for relevant items for this user. This will also tell you what the currency code and symbol is for this user.</p></figcaption></figure>

Once you have the prices available you can iterate through all items that have a price

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Get all item definitions that have a defined price valid for this user</p></figcaption></figure>

You can then read the current and base price for this user, note that current and base price are int64 (long) values. it is the base 100 value. e.g. $1.99 would be returned as 199.

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### [Start Purchase](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/start-purchase.md)

For items that have a valid price and are enabled for purchase in their item definition you can form the gate "start purchase" ... what this does is simply load the items into the Steam shopping cart and give you an Order and Transaction ID that represents that as of yet incomplete transaction.

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

As noted this "starts" the process but does not mean the transaction is completed. You can listen on the Micro Transaction Authorization Response event to know when a transaction is completed and check it against the Order ID provided in the Start Purchase process.

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Note that a transaction can fail or be cancelled... so its the "Authorized = True" that indicates this order is complete. Also, be aware the user may have changed the state of the shopping cart before completing the transaction so items may have been added or removed. It would be advisable to check the state of the inventory again or to listen to the Inventory Results Ready event and listen for changes to the player's inventory

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
