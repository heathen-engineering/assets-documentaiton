# Inventory

## Introduction

```csharp
public static class API.Inventory
```

The whole of the inventory system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Inventory.Client
```

To work with inventory from the point of view of a server you should use the Steam Web API for inventory.

{% embed url="https://partner.steamgames.com/doc/webapi/IInventoryService" %}

{% hint style="info" %}
This is a Service interface, methods in this interface should be called with the `input_json` parameter.
{% endhint %}

For more info on how to use the Steamworks Web API please see the [Web API Overview](https://partner.steamgames.com/doc/webapi\_overview).

### What can it do?

The Steam Inventory Service is a set of features that allow a game to enable persistent player inventories without having to run special servers to manage users or items.

The following is from the Steam Documentaiton for the Inventory feature.

> The Inventory Service can be used in two ways - either server-less or with the addition of a trusted server that knows game state.\
> \
> Without a game server, the game client can communicate directly to the steam service to retrieve users inventory contents, consume and exchange items, and receive new items granted as an effect of playtime. Users can also purchase items directly from the Item Store, or trade and exchange markets in the Steam community.\
> \
> However because the client can't be trusted (and the keys in a client can always be captured by an attacker) you can't give users specific items in this scheme. Rather you select certain items that can be dropped, and configure a drop frequency. At appropriate times, the game client invokes [Trigger Item Drop](inventory.md#undefined). Steam servers manage the playtime and drop frequency per-player. These APIs are called using an internal "Client API Key" that is assumed to be untrusted.\
> \
> If you have a participating trusted server then you can use a privileged Steam API key on the server and grant explicit items for appropriate situations. It is still important to keep in mind that you can't trust your own clients so you can only do this when the server is the master of the state of the game.\
> \
> Finally in conjunction with the Inventory Service you can sell an individual item or a cart of items, [in-game](https://partner.steamgames.com/doc/features/inventory/webfunctions#BuyItem) or through a web-based [storefront](https://partner.steamgames.com/doc/features/inventory/itemstore).\
> \
> Check out this presentation from [Steam Dev Days 2016](https://youtu.be/jDfhPTSOLis) for an implementation overview, details on the specific problems that the Inventory Service solves for developers.

See [Steam Inventory Service](https://partner.steamgames.com/doc/features/inventory) for more information.

## How To

{% hint style="success" %}
Methods that impact a user's inventory will typically have a [callback ](../../../../company/concepts/callbacks.md)that returns a type of [Inventory Result](../objects/inventory-result.md). In addition the [Item Definitions](../objects/item-definition.md) stored in the active Steam Settings will be updated with the resulting [Item Details](../objects/item-details.md) which be used as a real time view of the current state of the user's inventory.
{% endhint %}

{% hint style="info" %}
The [Item Definitions](../objects/item-definition.md) object contains shortcut methods to many of the features found in the API.Inventory interface.

For example it is possible to consume quantity, add promo items and exchange items directly from the item its self. Please review the [Item Definition](../objects/item-definition.md) object closely to understand all the options available to you.
{% endhint %}

### Add Promo Item

Grant a specific one-time promotional item to the current user.\
\
This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. This can be useful if your game has custom UI for showing a specific promo item to the user otherwise if you want to grant multiple promotional items then use [Add Promo Items](inventory.md#add-promo-items) or [Grant Prmo Items](inventory.md#undefined).\
\
Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```csharp
API.Inventory.Client.AddPromoItem(item, callback);
```

### Add Promo Items

Grant a specific one-time promotional item to the current user.\
\
This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. If you want to grant a single promotional item then use [Add Promo Item](inventory.md#add-promo-item). If you want to grant all possible promo items then use [Grant Promo Items](inventory.md#undefined).\
\
Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```
API.Inventory.Client.AddPromoItems(items, callback);
```

### Check Result Steam ID

Checks whether an inventory result handle belongs to the specified Steam ID.

{% hint style="warning" %}
This is important when using [Deserialize Results](inventory.md#undefined), to verify that a remote player is not pretending to have a different user's inventory.
{% endhint %}

```csharp
if(API.Inventory.Client.CheckResultSteamID(resultHandle, expectedId))
    Debug.Log("Yes");
else
    Debug.Log("No");
```

### Consume Item

Consumes items from a user's inventory. If the quantity of the given item goes to zero, it is permanently removed.

{% hint style="danger" %}
Once an item is removed it cannot be recovered.&#x20;

This is not for the faint of heart - if your game implements item removal at all, a high-friction UI confirmation process is highly recommended.
{% endhint %}

```
API.Inventory.Client.ConsumeItem(item, quantity, callback);
```

### Deserialize Results

Deserializes a result set and verifies the signature bytes.\
\
This call has a potential soft-failure mode where the handle status is set to [k\_EResultExpired](https://partner.steamgames.com/doc/api/steam\_api#k\_EResultExpired). [Get Result Items](inventory.md#get-result-items) will still succeed in this mode. The "expired" result could indicate that the data may be out of date - not just due to timed expiration (one hour), but also because one of the items in the result set may have been traded or consumed since the result set was generated. You could compare the timestamp from [Get Result Timestamp](inventory.md#undefined) to [ISteamUtils::GetServerRealTime](https://partner.steamgames.com/doc/api/ISteamUtils#GetServerRealTime) to determine how old the data is. You could simply ignore the "expired" result code and continue as normal, or you could request the player with expired data to send an updated result set.\
\
You should call [Check Result Steam ID](inventory.md#check-result-steam-id) on the result handle when it completes to verify that a remote player is not pretending to have a different user's inventory.

```
API.Inventory.Client.DeserializeResult(buffer, callback);
```

### Destroy Result

Destroys a result handle and frees all associated memory.

{% hint style="danger" %}
This only needs to be called if you are manually handling results ... which should not be happening if your using Heathen's Steamworks.



This is only provided for completness of the API to enable deep customization for those who wish to do so.
{% endhint %}

```
API.Inventory.Client.DestroyResult(resultHandle);
```

### Exchange Items

Grant one item in exchange for a set of other items.

This can be used to implement crafting recipes or transmutations, or items which unpack themselves into other items (e.g., a chest).

The caller of this API passes in the requested item and an array of existing items and quantities to exchange for it. The API currently takes an array of items to generate but at this time the size of that array must be 1 and the quantity of the new item must be 1.

Any items that can be granted MUST have an exchange attribute in their itemdef. The exchange attribute specifies a set of recipes that are valid exchanges for this item. Exchange recipes are evaluated atomically by the Inventory Service; if the supplied components do not match the recipe, or do not contain sufficient quantity, the exchange will fail.

{% hint style="warning" %}
It is much simpler to handle this feature through the Item Defenition object.



This is included in the API for completness sake
{% endhint %}

```csharp
API.Inventory.Client.ExchangeItems(itemsToGenerate,
                                   quantitiesToGenerate,
                                   instanceToDestroy,
                                   callback);
```

### Generate Items

{% hint style="warning" %}
For developer use only, this will only work if the authenticated Steam user is a member of the development team for this app.
{% endhint %}

Grants specific items to the current user, for developers only.

This API is only intended for prototyping - it is only usable by Steam accounts that belong to the publisher group for your game.

```
API.Inventory.Client.GenerateItems(items, quantity, callback);
```

### Get All Items

Start retrieving all items in the current users inventory.

{% hint style="info" %}
Calls to this function are subject to rate limits and may return cached results if called too frequently. It is suggested that you call this function only when you are about to display the user's full inventory, or if you expect that the inventory may have changed.
{% endhint %}

```
API.Inventory.Client.GetAllItems(callback);
```

### Get Eligible Promo Item IDs

Request the list of "eligible" promo items that can be manually granted to the given user.

These are promo items of type "manual" that won't be granted automatically. An example usage of this is an item that becomes available every week.

```
API.Inventory.Client.GetEligiblePromoItemDefinitionIDs(user, callback);
```

### Get Item Defiinition IDs

Returns the set of all item definition IDs which are defined in the App Admin panel of the Steamworks website.\
\
These item definitions may not necessarily be contiguous integers.\
\
This should be called in response to a [SteamInventoryDefinitionUpdate\_t](https://partner.steamgames.com/doc/api/ISteamInventory#SteamInventoryDefinitionUpdate\_t) callback. There is no reason to call this function if your game hardcodes the numeric definition IDs (eg, purple face mask = 20, blue weapon mod = 55) and does not allow for adding new item types without a client patch.

```csharp
API.Inventory.Client.GetItemDefinitionIDs(out SteamItemDef_t[] results);
```

### Get Result Items

Get the items assoceated with an inventory result handle.

{% hint style="danger" %}
You should never need to call this method if your using Heathen's Steamworks&#x20;



This method is included for completness of the interface.
{% endhint %}

```
API.Inventory.Client.GetResultItems(resultHandle, items, ref count);
```

### Get Result Timestamp

Gets the server time at which the result was generated.

{% hint style="danger" %}
This should never need to be called if your Heathen's Steamworks.



This method is included for completness of the interface.
{% endhint %}

### Grant Promo Items

Grant all potential one-time promotional items to the current user.\
\
This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. If you want to grant specific promotional items rather than all of them see: [Add Promo Item](inventory.md#add-promo-item) and [Add Promo Items](inventory.md#add-promo-items).\
\
Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```
API.Inventory.Client.GrantPromoItems(callback);
```

### Trigger Item Drop

Trigger an item drop if the user has played a long enough period of time.\
\
This period can be customized in two places:\


* At the application level within Inventory Service: Playtime Item Grants. This will automatically apply to all "playtimegenerator" items that do not specify any overrides.\

* In an individual "playtimegenerator" item definition. The settings would take precedence over any application-level settings.

\
Only item definitions which are marked as "playtime item generators" can be spawned.\
\
Typically this function should be called at the end of a game or level or match or any point of significance in the game in which an item drop could occur. The granularity of the playtime generator settings is in minutes, so calling it more frequently than minutes is not useful and will be rate limited in the Steam client. The Steam servers will perform playtime accounting to prevent too-frequent drops. The servers will also manage adding the item to the players inventory.

```
API.Inventory.Client.TriggerItemDrop(item, callback);
```
