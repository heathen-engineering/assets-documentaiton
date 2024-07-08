---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Inventory Item

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Inventory is a broad concept that helps you achieve a lot of very different design and mechanical requirements for your game. Its Steam Inventory would be used for microtransactions, loot boxes, player trading/community marketplace and secure consumables and crafting as well as for promotional items.

We have created a number of tools to help you represent your item types in your game project and to help you manage a view of your player's "inventory" that is to manage how much/many of what items they do or don't own and how they work with them.

You would start the process by defining your items in Steamworks Developer Portal and then for the items you will want/need to work with in game you can create an InventoryItemDataAsset Instance for each.

With your items created you can reference them in your Steam Game Instance and we can help you maintain a view of the "Item Details" ... item details are how Steam expresses instances of this item the player owns, how they are stacked and how many are in each stack.

## Create

Create a new Data Asset Instance of type InventoryItemDataAsset

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## Configure

Set the ID that you gave this item definition when you uploaded it to Steamworks Developer Portal.

{% hint style="info" %}
You can ignore the "Details" property for now, Details are set at run time as data is queried from Steam.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### Steam Game Instance

In your Steam Game Instance Blueprint, you will want to add each of your items to the Inventory Items array.

<figure><img src="../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Doing so allows our systems to update the Inventory Item Details of this data asset for you any time you use the "Simple" versions of inventory requests such as Get All Items - Simple

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

### Manual Detail Updates

Prefer to use manual operations against Steam Inventory?

We have you covered, the Steam Game Instance includes methods for clearing details and updating them based on results received from manual reads of an Inventory Result Handle.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## Use

To use an Item in your Blueprints you can simply create a variable of type InventoryItemDataAsset and set its default value to be the desired instance.

<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

You can now use the variable to work with this item type however you choose.

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
