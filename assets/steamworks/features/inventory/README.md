---
description: Hands down the larges and most complex of all Steam features
---

# Steam Inventory

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

First you should understand what Steam Inventory is and is not, the only real place to do so is via Valve's documentation and videos on the feature.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/inventory" %}

You will also need to understand the Steam Inventory Schema. While Heathen's tools help you define your item definitions in this schema, there will be time when you need to manually edit to take advantage of more complex features or to apply some unique concept specific to your project.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

## Required Reading

Steam Inventory can be used for consumables, craftables, player economy (marketplace and trading) and micro transactions. The system is concerned first and foremost with security and this can make it a more cumbersome feature than you need if your not taking advantage of either the player economy or MTX aspects of the system.

{% hint style="warning" %}
You can use Steam Inventory with no backend / trusted server at all, leveraging Valve's store and rules defined in the developer portal. This however does have restrictions such as not being able to "grant" a specific item at a specific time to a client. These restrictions are to insure security.

In short, a "client" can never be trusted so it can't do anything that cannot be validated by Valve. As a result items can only be generated for users via the PlayTimeGenerator feature, Promo feature or as part of a Steam Store or Steam Marketplace purchase (or trade).
{% endhint %}

{% hint style="info" %}
The following is taken directly from Valve's documentation. you should read Valves documentation.

[https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)
{% endhint %}

### Items

This is the most basic unit / object in Steam's Inventory system. An item is a defined concept with a unique ID, name, description and a range of additional metadata depending on the type of item it is and how it can be used. For example an item can have a "price" which makes it available on the Steam Store, it can also have an "exchange" defined allowing it to be crafted by consuming a given set of other items.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

### Bundles

This represents a set of items and quantities and when instantiated unpacks into the collection of items.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema#SpecifyBundles" %}

### Item Generators

This is a set of rules that will result in the production of an item. There are various types of generators, the most common used would be the PlayTimeGenerator which can be invoked to generate items for a player based on the amount of time the player has played the game.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

### Tags

A somewhat advanced feature, tags allow you to markup an item instance with additional data. For example your Iron Sword item could have a "Quality" tag with values such as "Quality:Common" or "Quality:Rare"

{% embed url="https://partner.steamgames.com/doc/features/inventory/itemtags" %}

### Tools

Tools are related to tags and allow you to create items that can modify other items, such as to change the tags on an item

{% embed url="https://partner.steamgames.com/doc/features/inventory/tools" %}

### Item Store

Your items can be sold to your player's via the item store. This requires the items to have a price or price category and is an optional feature.

{% embed url="https://partner.steamgames.com/doc/features/inventory/itemstore" %}

### Steam Community Market

Items can be made marketable by players, this allows player's to buy and sale items amongst themselves and results in a small cut of proceeds being relayed to you as the developer. See the `marketable` field on the Schema definition page.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

### Steam Trading

Items can be made tradeable by players, this allows player's to trade with each other over the Steam Inventory screen (out side your game). See the `tradable` field on the Schema definition page.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

