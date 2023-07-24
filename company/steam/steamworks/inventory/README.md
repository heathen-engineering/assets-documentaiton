---
description: Hands down the largest and most complex of all Steam features
---

# 📦 Inventory

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
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

### [Crafting](../../../../steam/crafting-system.md)

The Steam Inventory system has a concept of "exchange" wherein you can define a "recipe" being a collection of items and quantities that can be "exchanged" to receive a specific item.

The Exchange feature can be used to create loot boxes and other systems but far less predatory is the use as a crafting system. That is the player can collect reagents which you have defined as items and exchange them for specific items such as iron and leather to be exchanged for a shield or sword.

### [Microtransaction (MTX)](../microtransactions/)

Steam Inventory is the interface and framework you would use to define items for purchase either through the Steam store or through your store to be managed by Steam.

### Player Economy

Steam Inventory is how you create items that can be traded between players securely both in and out of the game and can optionally be put on the "Community Marketplace" for sale by players to players.

### [In-App Purchase (IAP)](../microtransactions/)

Steam Inventory is the framework you would use to define the items that can be purchased in-game and the exchange "recipes" that define how a player can "purchase" an item in-game for an in-game item e.g. in-game currency, in-game shop, etc.

### Item Collection / Progression

Steam Inventory is the framework you would use to define the items, reagents, crafting "recipes", drop rates and probability tables that drive item collection and item progression game loops in a secure manner

### In-game Economy

Steam Inventory is the framework you would use to define the items, reagents, recipes, drop rates, loot tables, etc. that drive these systems.&#x20;

No Steam Inventory items do not have to be available for sale, trade or community marketing you can hide them in inventory and control every aspect of how they are distributed, consumed and used. It is simply a secure way of defining the client's interaction with the items, the items themselves and related features of those items e.g. generators, drops, exchanges, etc.

## Item Definitions

Once you have created your Steam Inventory Items in the Steam Developer Portal you can access them in your project via code, through the [Item Data](../../../../assets/steamworks/data-layer/item-data.md) struct or the [Inventory API](../../../../assets/steamworks/api/inventory.md). You can also access your item definitions via Scriptable Objects using the Steam Settings object.

In all cases using your Item Defintiion you will be able to

* Determine if the user owns this item and how many they own
* Be able to start a purchase of this item
* Be able to consome this item
* Be able to use this item in an exchange recipie
* Be able to exchange other items (recipes) for this item
* Be able to read the item's price, name and other attributes if set

### Scriptable Objects

To import you Steam Inventory Item Definition into your project as Scriptable Objects you need to start your game in Editor so that the Steam API can initialize. Then open your Steam Settings in the inspector and click the Import option under the Inventory section

<figure><img src="../../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

This may take a few seconds to complete but it will import all [item definitions](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md) and create a Scriptable Object representation for each one stored under the Steam Settings object similar to Stas, Achievements and other Steam artifacts.

### Data Layer

In cases where you prefer to work in purse code or simply wish to avoid reference type objects such as Scriptable Objects you can use the Data Layer struct [Item Data](../../../../assets/steamworks/data-layer/item-data.md) to access your Item Definitions. As is always the case with the Data Layer you do not need to initialize or configure objects ahead of time. The Data Layer works on data without reference so you only need to know the uint ID of the item you wish to work with.

### API

The Data Layer as noted above is simply a struct that wraps around the underlying Inventory API. Some programmer centric developers may be more comfortable working with API end points than with structs and so you can access everything you need via the [Inventory.Client](../../../../assets/steamworks/api/inventory.md) API

## Required Reading

Steam Inventory can be used for consumables, craftables, player economy (marketplace and trading) and microtransactions. The system is concerned first and foremost with security and this can make it a more cumbersome feature than you need if you're not taking advantage of either the player economy or MTX aspects of the system.

{% hint style="warning" %}
You can use Steam Inventory with no backend / trusted server at all, leveraging Valve's store and rules defined in the developer portal. This however does have restrictions such as not being able to "grant" a specific item at a specific time to a client. These restrictions are to ensure security.

In short, a "client" can never be trusted so it can't do anything that cannot be validated by Valve. As a result, items can only be generated for users via the PlayTimeGenerator feature, Promo feature or as part of a Steam Store or Steam Marketplace purchase (or trade).
{% endhint %}

{% hint style="info" %}
The following is taken directly from Valve's documentation. you should read Valves documentation.

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

## Related Objects

The following are objects and tools in Steamworks Complete that can help you work with Steam Inventory.

### Inventory API

Learn more in our [Inventory API](../../../../assets/steamworks/api/inventory.md) documentation.

### Item Definition

Defines a Steam Inventory Item and provides access to commonly used features as well as the full definition of the item. You can learn more about the creation and use of [Item Definitions](./#item-definitions) in the section above.

### Item Detail

An object used to detail an instance of an item in the player's inventory. Learn more [here](../../../../assets/steamworks/objects/item-details.md).

## Sample Scenes

### 8 Inventory

This scene directs you to the documentation here and provides a simple example script that demonstrates the most common features.

### 9 Item Store Tutorial

This scene is meant to be used along with the [Item Store](../microtransactions/item-store/) article and demonstrates connecting [Item Definition](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md) objects to Unity UI.

## F.A.Q

### Generating Items

How do I generate or grant an item to a player at run time?

For testing a developer account can generate any item at runtime by simply calling the [GenerateItem](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#generate-item) method on the item definition or the corresponding command on the [Inventory API](../../../../assets/steamworks/api/inventory.md#generateitems).

This however will not work for players

{% hint style="warning" %}
Generate Item can only be used by developers for testing purposes.
{% endhint %}

For security reasons, there is no straightforward way to generate a specific item for the user from the Steam Client API. To give players items you need to do one of the following

* Promo Items\
  You can grant players items as part of a promotion. These are 1-time grants of free items and require the item to be configured as a "promo" item if done correctly you can use [AddPromoItem](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#add-promo-item) on the item definition or the corresponding command in the [Inventory API](../../../../assets/steamworks/api/inventory.md#addpromoitem) to grant the item.
* Drop Items\
  You can define play time generators that can be used to grant players items based on client-side rules ... mainly play time and or ownership of specific apps. This method requires you to configure a "Play Time Generator" with the required rules to drop the item and then to call [TriggerDrop](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#trigger-drop) on the item or the corresponding [Inventory API](../../../../assets/steamworks/api/inventory.md#triggeritemdrop) call.&#x20;
* Web API\
  You can use the Web API on a trusted web server to perform more direct actions like simply adding an item to a target player's inventory. This requires you to have a trusted web server using a publisher token on the Steam Web API. The Web API is out of scope for Unity assets as it's not part of Unity. You can learn more [here](https://partner.steamgames.com/doc/webapi/IInventoryService).

### In-Game Store

How do you create an in-game store for your items?

In the same way, you create any Unity UI, the visual and UI aspects of your store are wholly up to you. That is you being the developer know what items you have and should create a UI to present those to the player.

As to starting a purchase from your UI, you can use the [Start Purchase](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#start-purchase) command on the item definition or the corresponding [Inventory API](../../../../assets/steamworks/api/inventory.md#startpurchase) call.

If you're exchanging an item or group of items for another item e.g. in-game currency for an in-game item. then use the [Exchange](../../../../assets/steamworks/unity/scriptable-objects/item-definition.md#exchange) feature on the item definition or its corresponding [Inventory API](../../../../assets/steamworks/api/inventory.md#exchangeitems) call.

For more details see the [learning article here](./#item-store).

### Importing Generator Items

You will notice when importing Generator type items that Valve for some reason chose to hide the bundle aka "items" from the import. As such when importing Generator Items the content of the item will be blanked and you will need to manually redefine its content.

This is a limitation from Valve confirmed with Valve engineers as a deliberate limitation.

> Thanks for the additional context - it helps to see the results you're getting.
>
> I reached out to an engineer who worked on this API for some background. The GetItemDefinitionProperty API intentionally prevents the client from retrieving the bundle property of generator items. If the games you work with need in-game access to that data, they'll need to either include that information in their game builds or create some other service for retrieving it.
>
> Best,&#x20;
>
> Tavish

The above quote is from a Valve support case on this topic. It is not a bug nor a limitation we can effect. If you would like to see this changed you will need to raise it with Valve.

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/inventory/item-store" %}
