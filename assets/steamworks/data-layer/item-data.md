# Item Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct ItemData : IEquatable<ItemData>, 
                         IEquatable<int>, 
                         IEquatable<SteamItemDef_t>, 
                         IComparable<ItemData>, 
                         IComparable<int>, 
                         IComparable<SteamItemDef_t>
```

Provides easy access to detailed item information without needing a ScriptableObject. The ItemData structure can be implicitly converted from an int or item def meaning that if you know the ID of the item you want to work with you can get it without needing to look anything up.

Example:

```csharp
//Lets assume you have an item whoes ID is 100 and wanted to know how many the player
//owned of that item
var myItem = 100;
Debug.Log($"Player owns {myItem.GetTotalQuantity()}";
```

This of course assumes you have "Updated" the inventory at some point previously which can also be done using this structure.

```csharp
//This will ask Valve's Steam API to fetch all information about the player's 
//inventory items
ItemData.Update(HandleResult);
```

The HandleResult is an `Action<InventoryResult>` callback that will invoke when the process is complete and will provide you with detailed information on all the item instances found. Once that completes you can use the ItemData structure to work with your items.

## Fields and Attributes

### id

The id of this item

```csharp
public int id;
```

### ScriptableObject

Will return the scriptable object related to this item if any is known. This only has a value if you are using SteamSettings and have configured InventoryObjects.

```csharp
public ItemDefinitionObject ScriptableObject;
```

### Name

Gets the name of this item as it appears on the Steam store for this user.

```csharp
public string Name => get;
```

### Has Price

True if this item has a price recorded on the Steam store available to this user. This will only work after Request Prices has been called at least once.

```csharp
public bool HasPrice => get;
```

You can request prices using the ItemData as well

```csharp
ItemData.RequestPrice(HandleResult);
```

For more information see the RequestPrice method listed below.

### Currency Code

Get the currency code used by this user

```csharp
public static Currency.Code CurrencyCode => get;
```

### Currency Symbol

Gets the typical symbol used for the local user's currency e.g. $, €, £, etc.

```csharp
public static string CurrencySymbol => get;
```

### Current Price

Gets the current price displayed to this user as a base 100 ... for example 199 would be €1.99 assuming the user is using Euro.

```csharp
public ulong CurrentPrice => get;
```

### Base Price

Gets the base price of this item in the user's currency type, this is a base 100 ... for example 199 would be €1.99 assuming the user is using Euro.

```csharp
public ulong BasePrice => get;
```

## Methods

### Get Details

Returns a collection of ItemDetail which defines each "instance" of this item owned by this user.&#x20;

{% hint style="info" %}
Steam Inventory works with "item instances" you can think of an "instance" as being a stack or a "slot" in the inventory. Some item type can be stacked and so each "instance" may have a quantity from 0 to many. \
\
Thus the count of ItemDetails the user has does not necessarily equate to the "quantity" the user owns.
{% endhint %}

```csharp
public List<ItemDetail> GetDetails()
```

### Get Total Quantity

Returns the total number of this item that the user owns, that is this sums the "quantity" of every "instance" of this item the user owns.

```csharp
public long GetTotalQuantity()
```

### Add Promo Item

Grants this item to this user ... IF ... the item is a configured promotional item and the user qualifies for this promotion according to the rules you defined on the item definition.

```csharp
public bool AddPromoItem(Action<InventoryResult> callback)
```

The callback should be a method of the form

```csharp
void HandleCallback(InventoryResult result)
{
    //Do Work
}
```

### Get Consume Orders

Calculates a consume order that will consume the indicated number of this item ... if at all possible. This is meant to be used with the `Consume` method.

```csharp
public ConsumeOrder[] GetConsumeOrders(uint quantity)
```

### Consume

Consume 1 or more of this item, consume destroys the item and cannot be undone.

```csharp
public bool Consume(Action<InventoryResult> callback)
```

or

```csharp
public void Consume(ConsumeOrder order, Action<InventoryResult> callback)
```

or

```csharp
public void Consume(uint quantity, Action<InventoryResult> callback)
```

The first option assumes you wish to consume 1 item and does not require you to create any orders first.&#x20;

The second option should be used with `GetConsumeOrders`.

The final and third option will get consume orders for you based on the input quantity and process them in a background thread.

### Get Exchange Entry

This gets a collection of ExchangeEntry collections for a specified quantity of this item. This is meant to be used with the Exchange method.&#x20;

```csharp
public bool GetExchangeEntry(uint quantity, out ExchangeEntry[] entries)
```

For example if you wanted to exchange 10 of `itemA` for 1 of `itemB`.

```csharp
//Lets assume itemA has an ID of 101
ItemData itemA = 101;
//And itemB has an ID of 100
ItemData itemB = 100;

//First we see if the user owns 10 or more of itemA
if(itemA.GetExchangeEntry(10, out ExchangeEntry[] entries))
{
    //They do, so now we can exchange them for itemB
    itemB.Exchange(entries, HandleResult);
}
else
{
    //We come here if the user doesn't own enough
}
```

The HandleResult method would look like such.

```csharp
void HandleResult(InventoryResult result)
{
    //Do Work
}
```

### Exchange

Exchanges a collection of `ExchangeEntry` objects for 1 of this item type. This can be used to handle exchanging a loot box for the items inside, for crafting such as exchanging reagents for a crafted item, etc.

```csharp
public void Exchange(IEnumerable<ExchangeEntry> recipeEntries, Action<InventoryResult> callback)
```

See the [Get Exchange Entry](item-data.md#get-exchange-entry) method for an example of the usage.

### Generate Item

{% hint style="warning" %}
This will only work for users that are part of the development team for the project. It is meant for testing and debugging purposes only.
{% endhint %}

This generates a new item of this type in the users inventory.

```csharp
public void GenerateItem(Action<InventoryResult> callback)
```

or

```csharp
public void GenerateItem(uint quantity, Action<InventoryResult> callback)
```

### Start Purchase

If this item is valid for purchase this will add the item to the user's cart and open the cart in the Steam overlay so they can continue the purchase process.

```csharp
public void StartPurchase(Action<SteamInventoryStartPurchaseResult_t, bool> callback)
```

or

```csharp
public void StartPurchase(uint count, Action<SteamInventoryStartPurchaseResult_t, bool> callback)
```

### Get Price

Gets the current and base price as seen by the user. The values are returned in base 100 so a value of 199 would be €1.99 assuming a local currency of Euro.

```csharp
public void GetPrice(out ulong currentPrice, out ulong basePrice);
```

### Trigger Drop

If this item is configured as a "Play Time Generator" this will cause Valve's Steam to test the rules and timers and if available generate an item for the player.

```csharp
public void TriggerDrop(Action<InventoryResult> callback)
```

### Current Price String

Gets the formatted price string of this item ... assuming it has a price and that the prices have already been requested from Valve's Steam API.

This does account for the user's cultural formatting and currency code for example `€1.99` would be used in Ireland while `€1,99` would be used many other regions of Europe.

```csharp
public string CurrentPriceString()
```

### Base Price String

Gets the formatted price string of this item from the base price ... assuming it has a price and that the prices have already been requested from Valve's Steam API.

This does account for the user's cultural formatting and currency code for example `€1.99` would be used in Ireland while `€1,99` would be used many other regions of Europe.

```csharp
public string BasePriceString()
```

### Request Prices

Used to request prices from Valve's Steam API, this only needs to be called once and would usually be called in your bootstrap shortly after updating all items and of course after the Steam API had been initalized.

```csharp
public static void RequestPrices(Action<SteamInventoryRequestPricesResult_t, bool> callback)
```

### Update

Requests all inventory items from the Steam API and updates all item details based on the user's inventory. This should be called when you need to know the item states have all been updated recently such as just before opening an Inventory UI or similar.

```csharp
public static void Update(Action<InventoryResult> callback)
```

### Get

A set of simple helpers that will return the ItemData object related to the input you provide

```csharp
public static ItemData Get(int id)
```

or

```csharp
public static ItemData Get(SteamItemDef_t id)
```

or

```csharp
public static ItemData Get(ItemDefinitionObject item)
```
