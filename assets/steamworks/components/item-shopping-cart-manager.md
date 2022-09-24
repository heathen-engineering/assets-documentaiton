---
description: More than the Epic Game Store had at launch 🤪🤪
---

# Item Shopping Cart Manager

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This tool helps you manage a shopping cart like behaviour for in-game item shops working with [Steam Inventory](../troubleshooting-and-how-to-guides/inventory/). The tool can be used to add, set, or get items from the cart thus enabling you to add items, adjust the quantity in the cart and has features for reading the estimated total and reporting that as a string for display.

The core feature of the cart is its ability to manage an order, that is you can call StartPurchase through the cart and it will manage the process through to authorization. The idea is you would use the cart to start the purchase and listen for the result. You game should block further modification to the cart until the order is authorized or cleared.

## Events

### evtStartPurchaseError

```csharp
public StartPurchaseError evtStartPurchaseError;
```

This occurs when a request to start a purchase fails and indicates the reason why it failed. The handler for this event would look like this

```csharp
void HandleEvent(EResult result)
{
    //Do Work
}
```

The [EResult ](https://partner.steamgames.com/doc/api/steam\_api#EResult)is a standard Steam API feature you can find more information on it [here](https://partner.steamgames.com/doc/api/steam\_api#EResult).

### evtStartPurchaseSuccess

```csharp
public StartPurchaseSuccess evtStartPurchaseSuccess;
```

This occurs when a request to start a purchase was accepted by Steam. This does not indicate the purchase was completed simply that the request to start it was accepted. The handler for this event would look like this

```csharp
void HandleEvent(SteamInventoryStartPurchaseResult_t result)
{
    //Do Work
}
```

The [SteamInventoryStartPurcahseResult\_t ](https://partner.steamgames.com/doc/api/ISteamInventory#SteamInventoryStartPurchaseResult\_t)object is a standard Steam API concept you can find more information [here](https://partner.steamgames.com/doc/api/ISteamInventory#SteamInventoryStartPurchaseResult\_t).

### evtOrderAuthorization

```csharp
public OrderAuthorization evtOrderAuthorization
```

This occurs when Steam client notifies your game of a completed transaction and when that transaction order ID matches the pending order ID of this shopping cart. The handler for this would like this.

```csharp
void HandleEvent(ItemShoppingCartManager.ItemEntry[] itemsRequested, bool authorized)
{
    //Do Work
}
```

{% hint style="warning" %}
Keep in mind \
\
1 - The user may not have authorized the transaction so authorized will be false in this case.\
\
2 - The user can modify the items requested in Steam client so the items requested argument may not correspond exactly to what the user was issued.  \
\
Around the time this is raised assuming it was authorized you should also receive a [Inventory Changed](inventory-manager.md#evtchanged) event which should indicate what if any changes where made to the inventory.
{% endhint %}

## Fields and Attributes

### OrderPending

```csharp
public bool OrderPending => get;
```

True if the cart is currently tracking an order. The cart will ignore attempts to add or set items or start purchase while an order is pending. If you need to you can force the cart to clear the order via the ClearPending method.

### OrderId

```csharp
public ulong OrderId => get;
```

If an order is pending this will return the ID of that order, if not it will return 0

### TransacitonId

```csharp
public ulong TransactionId => get;
```

If an order is pending this will return the ID of that transaction, if not it will return 0

### items

```csharp
public List<ItemShoppingCartManager.ItemEntry> items
```

This is a collection of the items and quantities the cart has at current. This should not be updated while an order is pending.

## Methods

### Add

```csharp
public void Add(ItemDefinition item, int count)
```

Adds an item count to the items list. This is smart enough to "sum" the current amount of this item + the count you pass in. So if your cart already has 1 of this item and you add 2 more the cart will have 3 total. Adding a negative amount will reduce the quantity if the quantity reduces to zero or less the item will be removed from the list.

### Set

```csharp
public void Set(ItemDefinition item, int count)
```

Overwrites the quantity of an item in the list. This can be used to "type in" a quantity and if the value you pass in is zero or less it will remove the item from the list.

### Get

```csharp
public int Get(ItemDefinition item)
```

Reads the quantity for this item, if the item is not in the cart this will return 0.

### TotalPrice

```csharp
public ulong TotalPrice()
```

This gets the raw ulong price of the sum of the items in the cart. This is the same value that would be returned for each item's [CurrentPrice](../objects/item-definition.md#currentprice) value multiplied by the quantity for each item in the cart.

### TotalPriceSymbolledString

```csharp
public string TotalPriceSymbolledString()
```

This returns a string formatted based on the local currency code, for example "$10.99"

### TotalPriceCurrencyCodeString

```csharp
public string TotalPriceCurrencyCodeString()
```

This returns a string formatted based on the local currency code, for example "10.99 USD"

### StartPurchase

```csharp
public void StartPurchase()
```

or

```csharp
public void StartPurchase(Action<SteamInventoryStartPurchaseResult_t, bool> callback)
```

This starts a purchase process based on the items in the cart assuming there is no pending order. You can optionally pass in a callback handler that will be invoked when the process completes.

### ClearPending

```csharp
public void ClearPending(bool clearCart = false)
```

This tells the cart to forget about what ever order is pending. This generally shouldn't be used and does not "cancel" the order as Steam sees it. Thus its still possible that the order might complete later. The shopping cart will only respond to order authorization results for orders it is tracking as pending so if you clear the order it will simply ignore the notification that it was or was not authorized.

You can optionally clear the items in the cart when doing this.
