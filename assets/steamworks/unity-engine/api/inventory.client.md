# Inventory.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using InvClient = HeathenEngineering.SteamworksIntegration.API.Inventory.Client;
```

```csharp
public static class Inventory.Client
```

To work with inventory from the point of view of a server you should use the Steam Web API for inventory.

{% embed url="https://partner.steamgames.com/doc/webapi/IInventoryService" %}

{% hint style="info" %}
This is a Service interface, methods in this interface should be called with the `input_json` parameter.
{% endhint %}

For more info on how to use the Steamworks Web API please see the [Web API Overview](https://partner.steamgames.com/doc/webapi\_overview).

### What can it do?

The Steam Inventory Service is a set of features that allow a game to enable persistent player inventories without having to run special servers to manage users or items.

The following is from the Steam Documentation for the Inventory feature.

> The Inventory Service can be used in two ways - either server-less or with the addition of a trusted server that knows game state.\
> \
> Without a game server, the game client can communicate directly to the steam service to retrieve users inventory contents, consume and exchange items, and receive new items granted as an effect of playtime. Users can also purchase items directly from the Item Store, or trade and exchange markets in the Steam community.\
> \
> However because the client can't be trusted (and the keys in a client can always be captured by an attacker) you can't give users specific items in this scheme. Rather you select certain items that can be dropped, and configure a drop frequency. At appropriate times, the game client invokes [Trigger Item Drop](inventory.client.md#undefined). Steam servers manage the playtime and drop frequency per-player. These APIs are called using an internal "Client API Key" that is assumed to be untrusted.\
> \
> If you have a participating trusted server then you can use a privileged Steam API key on the server and grant explicit items for appropriate situations. It is still important to keep in mind that you can't trust your own clients so you can only do this when the server is the master of the state of the game.\
> \
> Finally in conjunction with the Inventory Service you can sell an individual item or a cart of items, [in-game](https://partner.steamgames.com/doc/features/inventory/webfunctions#BuyItem) or through a web-based [storefront](https://partner.steamgames.com/doc/features/inventory/itemstore).\
> \
> Check out this presentation from [Steam Dev Days 2016](https://youtu.be/jDfhPTSOLis) for an implementation overview, details on the specific problems that the Inventory Service solves for developers.

See [Steam Inventory Service](https://partner.steamgames.com/doc/features/inventory) for more information.

### Understanding Callbacks

A callback is a delegate similar to a UnityEvent, that is its a pointer to a method that will be called at some later point ... in the case of Steam methods it gets called when the process completes.

To learn more please read the article on [Callbacks](../../../../company/development/callbacks.md) and on [Lambda Expressions](../../../../company/development/lambda-expressions.md).

## Events

### Event Steam Inventory Definition Update

Triggered whenever item definitions have been updated, which could be in response to LoadItemDefinitions or any time new item definitions are available (eg, from the dynamic addition of new item types while players are still in-game).

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent()
{
}
```

Then you would register the event such as:

```csharp
API.Inventory.Client.EventSteamInventoryDefinitionUpdate.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behavior using it is destroyed

```csharp
void OnDestroy()
{
    API.Inventory.Client.EventSteamInventoryDefinitionUpdate.RemoveListener(HandleEvent);
}
```

### Event Steam Inventory Result Ready

This is fired whenever an inventory result transitions from k\_EResultPending to any other completed state, see GetResultStatus for the complete list of states. There will always be exactly one callback per handle.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(InventoryResult result)
{
}
```

Then you would register the event such as:

```csharp
API.Inventory.Client.EventSteamInventoryResultReady.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behavior using it is destroyed

```csharp
void OnDestroy()
{
    API.Inventory.Client.EventSteamInventoryResultReady.RemoveListener(HandleEvent);
}
```

### Event Steam Micro Transaction Authorization Responce

This is fired whenever Steam client notifies your game of a MTX transaction completing and includes details about that transaction. You can use this along side the [StartPurchase ](inventory.client.md#startpurchase)feature to know when a transaction starts and ends.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(AppId_t appId, ulong orderId, bool authorized)
{
}
```

Then you would register the event such as:

```csharp
API.Inventory.Client.EventSteamMicroTransactionAuthorizationResponce.AddListener(
                HandleEvent);
```

When you no longer need this handler you should remove it for example when the behavior using it is destroyed

```csharp
void OnDestroy()
{
    API.Inventory.Client.EventSteamMicroTransactionAuthorizationResponce.RemoveListener(
                HandleEvent);
}
```

## Methods

### AddPromoItem

Grant a specific one-time promotional item to the current user.

This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. This can be useful if your game has custom UI for showing a specific promo item to the user otherwise if you want to grant multiple promotional items then use AddPromoItems or GrantPromoItems.

Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```csharp
public static bool AddPromoItem(SteamItemDef_t itemDef, 
                                Action<InventoryResult> callback)
```

### AddPromoItems

Grant a specific one-time promotional item to the current user.

This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. If you want to grant a single promotional item then use AddPromoItem. If you want to grant all possible promo items then use GrantPromoItems.

Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```csharp
public static bool AddPromoItems(ItemDefinition item, 
                                Action<InventoryResult> callback)
```

```csharp
public static bool AddPromoItems(SteamItemDef_t[] itemDefs, 
                                Action<InventoryResult> callback)
```

```csharp
public static bool AddPromoItems(ItemDefinition[] items, 
                                Action<InventoryResult> callback)
```

```csharp
public static bool AddPromoItems(IEnumerable<SteamItemDef_t> itemDefs, 
                                Action<InventoryResult> callback)
```

### CheckResultSteamID

Checks whether an inventory result handle belongs to the specified Steam ID.

{% hint style="warning" %}
This is important when using [Deserialize Results](inventory.client.md#undefined), to verify that a remote player is not pretending to have a different user's inventory.
{% endhint %}

```csharp
public static bool CheckResultSteamID(SteamInventoryResult_t resultHandle, 
                                      CSteamID steamIDExpected)
```

### Consume Item

Consumes items from a user's inventory. If the quantity of the given item goes to zero, it is permanently removed.

{% hint style="danger" %}
Once an item is removed it cannot be recovered.&#x20;

This is not for the faint of heart - if your game implements item removal at all, a high-friction UI confirmation process is highly recommended.
{% endhint %}

```csharp
public static void ConsumeItem(SteamItemInstanceID_t itemConsume, 
                               uint quantity, 
                               Action<InventoryResult> callback)
```

### Deserialize Results

Deserializes a result set and verifies the signature bytes.\
\
This call has a potential soft-failure mode where the handle status is set to [k\_EResultExpired](https://partner.steamgames.com/doc/api/steam\_api#k\_EResultExpired). [Get Result Items](inventory.client.md#get-result-items) will still succeed in this mode. The "expired" result could indicate that the data may be out of date - not just due to timed expiration (one hour), but also because one of the items in the result set may have been traded or consumed since the result set was generated. You could compare the timestamp from [Get Result Timestamp](inventory.client.md#undefined) to [ISteamUtils::GetServerRealTime](https://partner.steamgames.com/doc/api/ISteamUtils#GetServerRealTime) to determine how old the data is. You could simply ignore the "expired" result code and continue as normal, or you could request the player with expired data to send an updated result set.\
\
You should call [Check Result Steam ID](inventory.client.md#check-result-steam-id) on the result handle when it completes to verify that a remote player is not pretending to have a different user's inventory.

```csharp
public static void DeserializeResult(byte[] buffer, 
                                Action<InventoryResult> callback)
```

### DestroyResult

Destroys a result handle and frees all associated memory.

{% hint style="danger" %}
This only needs to be called if you are manually handling results ... which should not be happening if your using Heathen's Steamworks.



This is only provided for completness of the API to enable deep customization for those who wish to do so.
{% endhint %}

```csharp
public static void DestroyResult(SteamInventoryResult_t resultHandle)
```

### ExchangeItems

Grant one item in exchange for a set of other items.

This can be used to implement crafting recipes or transmutations, or items which unpack themselves into other items (e.g., a chest).

The caller of this API passes in the requested item and an array of existing items and quantities to exchange for it. The API currently takes an array of items to generate but at this time the size of that array must be 1 and the quantity of the new item must be 1.

Any items that can be granted MUST have an exchange attribute in their itemdef. The exchange attribute specifies a set of recipes that are valid exchanges for this item. Exchange recipes are evaluated atomically by the Inventory Service; if the supplied components do not match the recipe, or do not contain sufficient quantity, the exchange will fail.

{% hint style="warning" %}
It is much simpler to handle this feature through the Item Defenition object.



This is included in the API for completness sake
{% endhint %}

```csharp
public static void ExchangeItems(SteamItemDef_t generate, 
                                SteamItemInstanceID_t[] destroy, 
                                uint[] destroyQuantity, 
                                Action<InventoryResult> callback)
```

### GenerateItems

{% hint style="warning" %}
For developer use only, this will only work if the authenticated Steam user is a member of the development team for this app.
{% endhint %}

Grants specific items to the current user, for developers only.

This API is only intended for prototyping - it is only usable by Steam accounts that belong to the publisher group for your game.

```csharp
public static void GenerateItems(SteamItemDef_t[] itemDefs, 
                                uint[] quantity, 
                                Action<InventoryResult> callback)
```

### GetAllItems

Start retrieving all items in the current users inventory.

{% hint style="info" %}
Calls to this function are subject to rate limits and may return cached results if called too frequently. It is suggested that you call this function only when you are about to display the user's full inventory, or if you expect that the inventory may have changed.
{% endhint %}

```csharp
public static void GetAllItems(Action<InventoryResult> callback = null)
```

### GetEligiblePromoItemIDs

Request the list of "eligible" promo items that can be manually granted to the given user.

These are promo items of type "manual" that won't be granted automatically. An example usage of this is an item that becomes available every week.

```csharp
public static void GetEligiblePromoItemDefinitionIDs(CSteamID userId, 
                                Action<SteamItemDef_t[], bool> callback)
```

### GetItemDefiinitionIDs

Returns the set of all item definition IDs which are defined in the App Admin panel of the Steamworks website.\
\
These item definitions may not necessarily be contiguous integers.\
\
This should be called in response to a [SteamInventoryDefinitionUpdate\_t](https://partner.steamgames.com/doc/api/ISteamInventory#SteamInventoryDefinitionUpdate\_t) callback. There is no reason to call this function if your game hardcodes the numeric definition IDs (eg, purple face mask = 20, blue weapon mod = 55) and does not allow for adding new item types without a client patch.

```csharp
public static bool GetItemDefinitionIDs(out SteamItemDef_t[] results)
```

### GetItemDefinitionProperty

Gets a property value for a specific item definition.

Note that some properties (for example, "name") may be localized and will depend on the current Steam language settings (see ISteamApps::GetCurrentGameLanguage). Property names are always ASCII alphanumeric and underscores.

```csharp
public static string GetItemDefinitionProperty(SteamItemDef_t item, 
                                               string propertyName)
```

### GetItemDefinitionProperties

Returns a list of the avilable properties on a given item

```csharp
public static string[] GetItemDefinitionProperties(SteamItemDef_t item)
```

### GetItemsByID

Gets the state of a subset of the current user's inventory.

```csharp
public static void GetItemsByID(SteamItemInstanceID_t[] instanceIds, 
                                Action<InventoryResult> callback = null)
```

### GetItemPrice

After a successful call to RequestPrices, you can call this method to get the pricing for a specific item definition.

```csharp
public static bool GetItemPrice(SteamItemDef_t item, 
                                out ulong currentPrice, 
                                out ulong basePrice)
```

### GetItemsWithPrices

After a successful call to RequestPrices, you can call this method to get all the pricing for applicable item definitions.

```csharp
public static bool GetItemsWithPrices(out SteamItemDef_t[] items, 
                                out ulong[] currentPrices, 
                                out ulong[] basePrices)
```

### GetResultItemProperty

Gets the dynamic properties from an item in an inventory result set.

```csharp
public static bool GetResultItemProperty(SteamInventoryResult_t resultHandle, 
                                uint itemIndex, 
                                string propertyName, 
                                out string valueBuffer, 
                                ref uint bufferSize)
```

### GetResultItems

Get the items associated with an inventory result handle.

```csharp
public static bool GetResultItems(SteamInventoryResult_t resultHandle, 
                                SteamItemDetails_t[] items, 
                                ref uint count)
```

### GetResultTimestamp

Gets the server time at which the result was generated.

```csharp
public static DateTime GetResultTimestamp(SteamInventoryResult_t resultHandle)
```

### GrantPromoItems

Grant all potential one-time promotional items to the current user.

```csharp
public static bool GrantPromoItems(Action<InventoryResult> callback = null)
```

### LoadItemDefinitions

Triggers an asynchronous load and refresh of item definitions.

```csharp
public static bool LoadItemDefinitions()
```

### RequestPrices

Request prices for all item definitions that can be purchased in the user's local currency. A SteamInventoryRequestPricesResult\_t call result will be returned with the user's local currency code. After that, you can call GetNumItemsWithPrices and GetItemsWithPrices to get prices for all the known item definitions, or GetItemPrice for a specific item definition.

```csharp
public static void RequestPrices(
        Action<SteamInventoryRequestPricesResult_t, bool> callback)
```

### SerializeItemResultsByID

Gets the state of a subset of the current user's inventory and serializes the data.

```csharp
public static void SerializeItemResultsByID(SteamItemInstanceID_t[] instanceIds, 
                                Action<byte[]> callback)
```

### SerializeAllItemResults

Start retrieving all items in the current users inventory and serializes the data.

```csharp
public static void SerializeAllItemResults(Action<byte[]> callback)
```

### StartPurchase

Starts the purchase process for the user, given a "shopping cart" of item definitions that the user would like to buy. The user will be prompted in the Steam Overlay to complete the purchase in their local currency, funding their Steam Wallet if necessary, etc.

```csharp
public static void StartPurchase(SteamItemDef_t[] items, 
        uint[] quantities, 
        Action<SteamInventoryStartPurchaseResult_t, bool> callback)
```

### TransferItemQuantity

Transfer items between stacks within a user's inventory.

```csharp
public static void TransferItemQuantity(SteamItemInstanceID_t source, 
        uint quantity, 
        SteamItemInstanceID_t destination, 
        Action<InventoryResult> callback)
```

### TriggerItemDrop

Trigger an item drop if the user has played a long enough period of time.

```csharp
public static void TriggerItemDrop(SteamItemDef_t item, 
        Action<InventoryResult> callback)
```

### StartUpdateProperties

Starts a transaction request to update dynamic properties on items for the current user. This call is rate-limited by user, so property modifications should be batched as much as possible (e.g. at the end of a map or game session). After calling SetProperty or RemoveProperty for all the items that you want to modify, you will need to call SubmitUpdateProperties to send the request to the Steam servers. A SteamInventoryResultReady\_t callback will be fired with the results of the operation.

```csharp
public static SteamInventoryUpdateHandle_t StartUpdateProperties()
```

### SubmitUpdateProperties

Submits the transaction request to modify dynamic properties on items for the current user. See StartUpdateProperties.

```csharp
public static void SubmitUpdateProperties(SteamInventoryUpdateHandle_t handle, 
        Action<InventoryResult> callback)
```

### RemoveProperty

Removes a dynamic property for the given item.

```csharp
public static void RemoveProperty(SteamInventoryUpdateHandle_t handle, 
                                SteamItemInstanceID_t item, 
                                string propertyName)
```

### SetProperty

Sets a dynamic property for the given item. Supported value types are strings, boolean, 64 bit integers, and 32 bit floats.

```csharp
public static void SetProperty(SteamInventoryUpdateHandle_t handle, 
                SteamItemInstanceID_t item, 
                string propertyName, 
                string data)
```

```csharp
public static void SetProperty(SteamInventoryUpdateHandle_t handle, 
                SteamItemInstanceID_t item, 
                string propertyName, 
                bool data)
```

```csharp
public static void SetProperty(SteamInventoryUpdateHandle_t handle, 
                SteamItemInstanceID_t item, 
                string propertyName, 
                long data)
```

```csharp
public static void SetProperty(SteamInventoryUpdateHandle_t handle, 
                SteamItemInstanceID_t item, 
                string propertyName, 
                float data)
```

### GetExtendedItemDetail

Constructs an [ItemDetail](../objects/item-detail.md) object based on a native SteamItemDetails\_t object and its source result list

```csharp
public static ItemDetail GetExtendedItemDetail(SteamInventoryResult_t result, 
                                uint index, 
                                SteamItemDetails_t detail)
```

## How To

{% hint style="success" %}
Methods that impact a user's inventory will typically have a [callback ](../../../../company/development/callbacks.md)that returns a type of [Inventory Result](../objects/inventory-result.md). In addition the [Item Definitions](../../unity/scriptable-objects/item-definition.md) stored in the active Steam Settings will be updated with the resulting [Item Details](../objects/item-detail.md) which be used as a real time view of the current state of the user's inventory.
{% endhint %}

{% hint style="info" %}
The [Item Definitions](../../unity/scriptable-objects/item-definition.md) object contains shortcut methods to many of the features found in the API.Inventory interface.

For example it is possible to consume quantity, add promo items and exchange items directly from the item its self. Please review the [Item Definition](../../unity/scriptable-objects/item-definition.md) object closely to understand all the options available to you.
{% endhint %}

### Add Promo Item

Grant a specific one-time promotional item to the current user.\
\
This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. This can be useful if your game has custom UI for showing a specific promo item to the user otherwise if you want to grant multiple promotional items then use [Add Promo Items](inventory.client.md#add-promo-items) or [Grant Prmo Items](inventory.client.md#undefined).\
\
Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```csharp
API.Inventory.Client.AddPromoItem(item, callback);
```

### Add Promo Items

Grant a specific one-time promotional item to the current user.\
\
This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. If you want to grant a single promotional item then use [Add Promo Item](inventory.client.md#add-promo-item). If you want to grant all possible promo items then use [Grant Promo Items](inventory.client.md#undefined).\
\
Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item list a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```
API.Inventory.Client.AddPromoItems(items, callback);
```

### Check Result Steam ID

Checks whether an inventory result handle belongs to the specified Steam ID.

{% hint style="warning" %}
This is important when using [Deserialize Results](inventory.client.md#undefined), to verify that a remote player is not pretending to have a different user's inventory.
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
This call has a potential soft-failure mode where the handle status is set to [k\_EResultExpired](https://partner.steamgames.com/doc/api/steam\_api#k\_EResultExpired). [Get Result Items](inventory.client.md#get-result-items) will still succeed in this mode. The "expired" result could indicate that the data may be out of date - not just due to timed expiration (one hour), but also because one of the items in the result set may have been traded or consumed since the result set was generated. You could compare the timestamp from [Get Result Timestamp](inventory.client.md#undefined) to [ISteamUtils::GetServerRealTime](https://partner.steamgames.com/doc/api/ISteamUtils#GetServerRealTime) to determine how old the data is. You could simply ignore the "expired" result code and continue as normal, or you could request the player with expired data to send an updated result set.\
\
You should call [Check Result Steam ID](inventory.client.md#check-result-steam-id) on the result handle when it completes to verify that a remote player is not pretending to have a different user's inventory.

```
API.Inventory.Client.DeserializeResult(buffer, callback);
```

### Destroy Result

Destroys a result handle and frees all associated memory.

{% hint style="danger" %}
This only needs to be called if you are manually handling results ... which should not be happening if your using Heathen's Steamworks.



This is only provided for completeness of the API to enable deep customization for those who wish to do so.
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
It is much simpler to handle this feature through the Item Definition object.



This is included in the API for completeness sake
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

Get the items associated with an inventory result handle.

{% hint style="danger" %}
You should never need to call this method if your using Heathen's Steamworks&#x20;



This method is included for completeness of the interface.
{% endhint %}

```
API.Inventory.Client.GetResultItems(resultHandle, items, ref count);
```

### Get Result Timestamp

Gets the server time at which the result was generated.

{% hint style="danger" %}
This should never need to be called if your Heathen's Steamworks.



This method is included for completeness of the interface.
{% endhint %}

### Grant Promo Items

Grant all potential one-time promotional items to the current user.\
\
This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. If you want to grant specific promotional items rather than all of them see: [Add Promo Item](inventory.client.md#add-promo-item) and [Add Promo Items](inventory.client.md#add-promo-items).\
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
