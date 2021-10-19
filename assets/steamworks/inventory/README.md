---
description: >-
  Leverage Steam Inventory to create a player economy through marketplace, trade
  and more. Deliver secure crafting systems, create consumables or drive
  microtransacitons as part of the Steam Store.
---

# Inventory

## **Introduction**

First you should understand what Steam Inventory is and is not, the only real place to do so is via Valve's documentation and videos on the feature.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/inventory" %}

You will also need to understand the Steam Inventory Schema. While Heathen's tools help you define your item definitions in this schema, there will be time when you need to manually edit to take advantage of more complex features or to apply some unique concept specific to your project.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

The Steamworks kit provides you with tools to do this quickly and easily while also setting up the data model in your game so your game logic can use it. Before we get started, here are a few terms and concepts

![](<../../../.gitbook/assets/image (28).png>)

### **Steam Inventory**

This is a service provided by Valve where in you can define a data model, aka a schema, aka the shape of items that Valve will manage in the player’s Steam Inventory - same place trading cards and coupons go. As you may know Steam Inventory Items can be trade-able, meaning players can give them to each other and they can be made marketable, meaning players can sell them to each other for real money. Also Steam Items can be sold by the developer on the Steam store e.g. MTX (Micro transaction)

### **Item Def**

This refers to the JSON data as seen in the Steam Developer Portal.

The JSON can be generated from the Inventory Editor window by clicking the `Generate JSON` button located in the upper right corner of the window.

### **Item Data**

This refers to the Scriptable Objects defined in Unity that represent the items defined in your Item Def JSON.

All of the items located along the left side of the Inventory Editor window are your `Item Data` objects, and can represent individual items, bundles, generators, tag generators and may have 1 or more recipes associated with them.

When you select one of these `Item Data` objects you can edit its settings in the main area of the Inventory Editor window. These settings will be exported on generation of JSON

## Features

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

