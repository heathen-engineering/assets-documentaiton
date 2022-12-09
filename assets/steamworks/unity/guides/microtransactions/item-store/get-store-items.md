# Get Store Items

<figure><img src="../../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

How do you know what items to display in a store?

Well honestly you should know this at development time and shouldn't be doing this in code as its far less performant and far more error prone. That is as a developer you already know what items your app has when you code them so why not go ahead and code the store accordingly?

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

That said you can do it programmatically and here is how.

## Refresh your Item Definitions

```csharp
API.Inventory.Client.LoadItemDefinitions();
```

Read more [here](../../../../api/inventory.md#loaditemdefinitions).

In short this starts the process of loading item definitions from Steam and will trigger the [EventSteamInventoryDefinitionUpdate](../../../../api/inventory.md#eventsteaminventorydefinitionupdate) to be raised when the definitions are ready.

You would do this as soon as Steam Initializes so you can pull the current item definitions local.

## Iterate and Initialize

Once the [EventSteamInventoryDefinitionUpdate ](../../../../api/inventory.md#eventsteaminventorydefinitionupdate)has been raised and you have the item definitions local to the user's cash you can walk the items and spawn UI objects to represent each.

```csharp
foreach(var itemDefinition in SteamSettings.Client.inventory.items)
{
    //Instantiate your UI here for this item
}
```

For each item you will need to get some common information.&#x20;

* Item Name\
  You can find this in [item\_name](../../../scriptable-objects/item-definition.md#item\_name). or by using the [DisplayName](../../../scriptable-objects/item-definition.md#displayname) field of Item Definition.
* Item Description\
  You can find this in [item\_description](../../../scriptable-objects/item-definition.md#item\_description).
* Price\
  If you want to fetch the price in the user's currency see: [Current Price](../../../scriptable-objects/item-definition.md#currentprice) and [Base Price](../../../scriptable-objects/item-definition.md#baseprice). You can check if there is a price at all via [Has Price](../../../scriptable-objects/item-definition.md#hasprice).
* Images\
  Several images can be associated with an item ... we don't recommend using any of them as they should all be optimized for use in web and thus of pore quality for use in game. but you can read them from the item definition via
  * Icon URL\
    `itemDef.item_icon`\_`url`
  * Large Icon URL\
    `itemDef.item_icon_url_large`
  * Store  Images\
    `foreach(var imageUrl in itemDef.item_store_images)`
* Recipies\
  To detect if this item can be exchanged for and if so what it requires you need to read the [item\_exchange](../../../scriptable-objects/item-definition.md#item\_exchange).
