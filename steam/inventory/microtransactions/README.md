---
description: Aka MTX, IAP, In App Purchase, cash shop, etc.
---

# 💸 Microtransactions

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Steam Microtransactions (In-Game Purchases) are handled via the [Steam Inventory](../../../company/steam/steamworks/inventory/) feature.&#x20;

{% hint style="info" %}
Have a look at our articles on [Monetization ](../../../company/design/monetization/)before you get started designing your game's monetization systems.&#x20;

[https://kb.heathenengineering.com/company/concepts/monetization](https://kb.heathenengineering.com/company/concepts/monetization)
{% endhint %}

## Quick Start

### Step 1: Design

Do not skip this part.

Before you start creating your item definitions and store UI. You need to first understand the Steam Inventory schema. Understand what types of items you can define, and then you need to design your solution based on Steam Inventory features and your requirements.&#x20;

By design we mean design what items, generators, promos, bundles and tags your game will need, what exchange recipes will be used and what drop rules you will use.

With Steam Inventory you can easily create an item definition, but once created you can not delete it. You can change its settings, even hide it, but you cannot delete it.

To learn more about the types of items, the schema they are defined with and how to define them see the [Inventory article](../../../company/steam/steamworks/inventory/).

### Step 2: Define

Once you have designed your solution and understand what items, generators, bundles, etc. you will need, it's time to define those items. You must define the items in an item definition file using a JSON structure and upload that to the Steam Developer Portal.

Heathen has tools and guidance to help you with this process. Please read the [Item Definition Tools article](../item-definition-tools.md) for more information.

### Step 3: Use

With your items designed and defined you are effectively done. If you defined your items with a price and did not mark them as Store Hidden then they will appear in your App's Item store on the Steam client.

Users can browse and purchase items for your game directly through the Steam store. Valve will handle payment processing and deliver the items to the user's inventory. You can detect what items a user owns in the game by referencing your [Item Definition](../../../company/steam/steamworks/inventory/#item-definition) and using its feature to see the quantity.

You can also set up an in-game store using your Item Definition and the Start Purchase option. Heathen even has an [Item Shopping Cart Manager](../../../assets/steamworks/unity/components/item-shopping-cart-manager.md) to help you set up and manage an in-game shopping cart ... so your game can be a step or two better than the Epic Game Store was at launch :wink:

## In-Game Store

Please see the [Item Store](item-store/) article and its sub-articles for more information on how to set up an in-game store using Steam Inventory.

## In-Game Currency

Setting up a cash shop is as easy as assigning a price to the items, you can also though set up an in-game currency where they player "purchases" items via an in-game currency.

This is effectively "crafting" that is your in-game currency is a reagent that is exchanged for another item.

See the [Crafting System](../crafting-system.md) article for more information.
