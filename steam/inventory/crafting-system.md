# 🔨 Crafting System

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The [Steam Inventory](../../company/steam/steamworks/inventory/) feature of Steamworks has a system for "exchange" that is you can define a "recipe" of items that can be exchanged for another item. This system enables a number of features such as in-game shops but also of course traditional crafting.

Exchanges are flexible - using a key to open a crate, building a fancy item out of component parts, item recycling, and item upgrades can all be achieved with the crafting aka exchange system.

## Quick Start

When crafting or using exchange, you are providing a list of material items to be exchanged for the target item. The server will check each recipe, and choose the first recipe that is satisfied by the materials given. The item that is crafted may be a regular [item](../../company/steam/steamworks/inventory/#items), [bundle](../../company/steam/steamworks/inventory/#bundles) or [generator](../../company/steam/steamworks/inventory/#item-generators).

### Step 1: Design

Do not skip this part.

Before you start creating your items and reagents, you need to first understand the Steam Inventory schema. Understand what types of items you can define, and then you need to design your solution based on Steam Inventory features and your requirements.&#x20;

By design we mean design what items, generators, promos, bundles and tags your game will need, what exchange recipes will be used and what drop rules you will use.

With Steam Inventory you can easily create an item definition, but once created you can not delete it. You can change its settings, even hide it, but you cannot delete it.

To learn more about the types of items, the schema they are defined with and how to define them see the [Inventory article](../../company/steam/steamworks/inventory/).

### Step 2: Define

Once you have designed your solution and understand what items, generators, bundles, etc. you will need, it's time to define those items. You must define the items in an item definition file using a JSON structure and upload that to the Steam Developer Portal.

Heathen has tools and guidance to help you with this process. Please read the [Item Definition Tools article](item-definition-tools.md) for more information.

### Step 3: Use

Once you have defined your items and reagents, exchanging items via code in your game is a simple process.&#x20;

The steps of exchange are as follows

* &#x20;Get references to the specific items that will be exchanged\
  You can use the Get Exchange Entry for this step
  * [Item Definition Get Exchange Entry](../../toolkit-for-steamworks-sdk/unity/scriptable-objects/item-definition.md#get-exchange-entry)
  * [Item Data Get Exchange Entry](../../toolkit-for-steamworks-sdk/unity/classes-and-structs/item-data.md#get-exchange-entry)
  * [Inventory API Get Exchange Entry](../../toolkit-for-steamworks-sdk/unity/api/inventory.client.md#exchange-items)
* On the item you wish to "craft" exchange the reagents you just collected\
  You can use the Exchange feature for this step
  * [Item Definition Exchange](../../toolkit-for-steamworks-sdk/unity/scriptable-objects/item-definition.md#exchange-1)
  * [Item Data Exchange](../../toolkit-for-steamworks-sdk/unity/classes-and-structs/item-data.md#exchange)
  * [Inventory API Exchange](../../toolkit-for-steamworks-sdk/unity/api/inventory.client.md#exchange-items)

## Definition Recipes

You define recipes on the item that will be crafted. A recipe will specify what items or tags are required and in what quantity. Recipes can consume a specific item or any item with a given tag.

The item that is crafted may be a regular [item](../../company/steam/steamworks/inventory/#items), [bundle](../../company/steam/steamworks/inventory/#bundles) or [generator](../../company/steam/steamworks/inventory/#item-generators). That means you can have the user craft a specific sword for example, or they "salvage" a sword to craft a bundle of iron, leather, etc. or you could exchange a resource for a random reward such as a loot box by having the "craft" an item generator.

The [Item Definition Tools](item-definition-tools.md) provided by Setamworks Complete can assist you in creating properly formatted recipes for your items.

The JSON format for an exchange is as follows:

```json
<exchange>: <recipe> { ";" <recipe> }
<recipe>: <material> { "," <material> }
<material>: <item_def_descriptor> / <item_tag_descriptor>
<item_def_descriptor>: <itemdefid> []
<item_tag_descriptor>: <tag_name> ":" <tag_value> []
```

The above is taken from Valve's documentation here: [Exchange Format](https://partner.steamgames.com/doc/features/inventory/schema#ExchangeFormat).

It says that&#x20;

```json
"exchange" : <recipie>
```

where recipe is a collection separated by `;`

so in effect

```json
"exchange" : <recipie>;<recipe>;<recipe>
```

The recipe itself is defined on line 2 of the format example

```json
<recipe> : <material> { "," <material> }
```

This is saying that the recipe is a collection of \<material> separated by `;`

so in effect, this would be 2 separate recipes with 2 requirements each

```json
"exchange" : <material>,<material>;<material>,<material>
```

Next the format defines \<material> as being either a item definition descriptor or a tag descriptor.

Item definition descriptor it defines as an array of item IDs following the same format as all item ID arrays in the schema e.g. \<id>x\<quantity>

```csharp
"exchange" : "100x4"
```

And the tag descriptor using the standard tag array e.g. \<tag:value>\*\<quantity>

```json
"exchange" : "quality:common*4"
```

### Examples

The following recipe would require one of the following to be true

* 1 item ID 100 and 1 item ID 101
* 5 item ID 203
* 3 Item ID 103 and 3 Item ID 104

```json
"exchange":"100,101;102x5;103x3,104x3"
```

You can also use [tags](../../company/steam/steamworks/inventory/#tags) in a recipe, the following recipe requires that the reagents provided have a `handed:left` tag and a `handed:right` tag such as exchanging one left and one right-handed glove.

```json
"exchange":"handed:left,handed:right"
```

You can require a quantity of tags as well though we don't use x in this case rather \* for example the following requires 3 `type:tree` tags and 1 `quality:fancy` tag.

```json
"exchange":"type:tree*3,quality:fancy"
```

## Unity Examples

To craft an item ... that is to exchange a set of materials/reagents for an item. we do the following

### Using Item Definition

Read the [Item Definition article's Exchange](../../toolkit-for-steamworks-sdk/unity/scriptable-objects/item-definition.md#exchange-1) section for a detailed example.

### Using Item Data

Read the [Item Data article's Exchange](../../toolkit-for-steamworks-sdk/unity/classes-and-structs/item-data.md#exchange-items) section for a detailed example.

## Unreal Examples

[Exchange Items](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/exchange-items.md) lets you pass in an array of [Item Count](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/types/item-count.md) to exchange for a given item. The callback works much like the [Get All Items](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-all-items.md) discussed in the [Inventory](../../company/steam/steamworks/inventory/) article.

To use the feature you first need to know what item ID you want to "craft" i.e. exchange other items for.&#x20;

Next, you need to know the instance ID and count of each item you will be exchanging. You typically get the Instance IDs from the Get All Items request but you can for example cascade crafting requests.

An example of a cascaded crafting request would be to craft Iron Ore into Iron Bars and then craft the Iron Bars into an Iron Sword. That is your exchanging 1 or more Ore items for Bars and 1 or more Bars for Sword.

The following image is an example of creating the "recipe" array needed by the Exchange Items node. In this example, we assumed we needed 15 of some item and if we had 2 stacks of 10 each with IDs of 123 and 124 respectively then the below "Make Array" node would be the correct recipe.

In the example, we are using all of stack 123 and 5 from stack 124.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>
