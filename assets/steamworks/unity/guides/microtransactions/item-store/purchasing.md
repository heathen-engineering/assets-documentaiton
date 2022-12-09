# Purchasing

<figure><img src="../../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

So now you have your items listed and displaying relevant visuals and information. You now need to respond to use input to start a purchase with real currency or to exchange in-game items aka in-game currency.

You can see a simple working example of this in the Example Item Behaviour.

## Start Purchase

This is done when you want to send the user to the Steam Store page so they can "check out" spending real money on some item. Note you can call Start Purchase on a single item or you can set up a shopping cart building up a collection of items and call Start Purchase on all of them.

### [Item Shopping Cart Manager](../../../components/item-shopping-cart-manager.md)

We have constructed a tool to help you manage a shopping cart in game. This tool is capable of adding, removing and editing the quantities of items in it, it can report the estimated total of the cart and can manage and track the purchase operation through to authorization reporting issues and or successes through simple Unity events.

You would add this script to your Store/Shop UI and use its members to add, remove and edit the items in the cart. Once you have populated the cart and are ready to "check out" you can call StartPurchase in the manager to kick off the process and track the results. To learn more about the use of [Item Shopping Cart Manager see this article](../../../components/item-shopping-cart-manager.md).

### Manual

You can of course call start purchase your self and handle the response. The following code demonstrates a StartPurchase on a single item and uses the [ItemDefinition.StartPurchase](../../../scriptable-objects/item-definition.md#start-purchase) method to simplify the process.

```csharp
public void StartPurchase()
{
    itemDefinition.StartPurchase((responce, ioError) =>
    {
        if (!ioError)
        {
            if (responce.m_result == EResult.k_EResultOK)
            {
                Debug.Log("Start purchase completed");
                //You should store the order ID if you want to track its completion
                StoreController.orderId = responce.m_ulOrderID;
            }
            else
            {
                Debug.LogError("Unexpected result from Valve: " + responce.m_result);
            }
        }
        else
        {
            Debug.LogError("Valve indicated an IO Error occured. i.e. failed to start the process at all.");
        }
    });
}
```

You can also start purchase on a set of items, the following is the code from our Shopping Cart tool and how it handles this use case.

```csharp
//Remove any empty or null items
items.RemoveAll(p => p.item == null || p.quantity <= 0);
//Create a buffer for the item types
var itemDefs = new Steamworks.SteamItemDef_t[items.Count];
//A buffer for the item quantities
var itemQuan = new uint[items.Count];
//Populate the buffers from our cart
for (int i = 0; i < items.Count; i++)
{
    var entry = items[i];
    itemDefs[i] = entry.item.Id;
    itemQuan[i] = entry.quantity <= 0 ? 0 : (uint)(entry.quantity);
}
//Start the purcahse
API.Inventory.Client.StartPurchase(itemDefs, itemQuan, (result, error) =>
{
    if(error)
    {
        //Report the IO Error
        Debug.LogError($"StartPurchase - IO Error reported by Steam");
        evtStartPurchaseError.Invoke(EResult.k_EResultIOFailure);
    }
    else
    {
        if (result.m_result != EResult.k_EResultOK)
        {
            //Report the Result Error
            Debug.LogError($"StartPurchase - Error reported by Steam: {result.m_result}");
            evtStartPurchaseError.Invoke(result.m_result);
        }
        else
        {
            //Record the result so we can process the auth responce later
            _result = result;
            evtStartPurchaseSuccess.Invoke(result);
        }
    }

    callback?.Invoke(result, error);
});
```

Assuming you want to track the completion of the order you should listen on the Micro Transaction Authorization Response. You can find this on the [Inventory Manager](../../../components/inventory-manager.md#evttransactionresponce) component or directly in the [Inventory API](../../../../api/inventory.md#eventsteammicrotransactionauthorizationresponce). In either case this is an event that is raised when the Steam client informs your game of a completed e.g. authorization on a transaction. The event will indicate the app the transaction is for, the order ID of the transaction and rather or not the transaction was authorized.

## Exchange

Its fairly common to have user's "purchase" items with an in-game currency. In reality this is not a purchase it is an exchange. That is it is similar to crafting where in some reagents are exchanged for some other item. Exchanges must be done one item at a time and the following code snippet shows how you would go about doing that for a given [itemDefinition](../../../scriptable-objects/item-definition.md).

```csharp
public void Exchange()
{
    //This assumes the linked item has a recipie
    if (itemDefinition.CanExchange(itemDefinition.item_exchange.recipe[0], out List<ExchangeEntry> recipe))
    {
        //If the user owns the required items to satisfy the recipie defined in the first index of the recipies 
        //then go ahead and exchange for it

        itemDefinition.Exchange(recipe, (responce) =>
        {
            if (responce.result == EResult.k_EResultOK)
            {
                Debug.Log("Exchange completed");
            }
            else
            {
                Debug.LogError("Unexpected result from Valve: " + responce.result);
            }
        });
    }
    else
    {
        Debug.LogWarning("The user does not own the required items to perform this exchange");
    }
}
```

The first step in this process is the CanExchange check.

```csharp
if (itemDefinition.CanExchange(itemDefinition.item_exchange.recipe[0],
                               out List<ExchangeEntry> recipe))
```

[CanExchange ](../../../scriptable-objects/item-definition.md#can-exchange)is a method on the [Item Definition](../../../scriptable-objects/item-definition.md) and takes a given recipe as an input and has an output that collects the required items to complete the recipe.

Assuming this returns true then we can complete an exchange for this item on this recipe, so the next step is to request that using the output the [CanExchange](../../../scriptable-objects/item-definition.md#can-exchange) method provided us. Unlike StartPurchase we will know in a single step rather or not this was a success and the items will already be updated.
