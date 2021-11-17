---
description: BGSDK Wallet Examples
---

# Read the user's wallets

## Interoduction

For more information on Wallets please refer to the Wallet API article

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/api/wallets" %}

Accessing the user's wallet is likely the main use for the BGSDK in your game or app. Tokens aka "NFTs" or "Fungibles" typically represent some object or property the user can have that is related to your app or game, such as an item (Iron Sword, Tabby Cat, Box of Stuff, etc.), character (pets, companion, etc), title (Champion, Heretic, General Do-Gooder, etc.) or permission (Founder, Supporter, Backer, World First Dungeon Raider, etc.)

These tokens represent license to a thing in your game, and this license can be exchanged between players in or out side of your game. The Venly wallet system helps control access to these items, and simplifies minting and exchange of these items. The BGSDK makes it easy to determine what "items" if any your player owns. It does this by reading the player's wallets.

{% hint style="info" %}
Ownership of a token represents license of something related to or in your game that is transferable. Your game must read what licenses the current user owns and use that ownership to unlock or grant the related in game effects.

This distinction is important, the Token Type "Iron Sword" for example would not be an iron sword in your game, rather it is a transferable license that indicates that the owner has rights to something , apparently, an Iron Sword. That right can be transferred to other player's and could in theory be read by other games to grant other in game effects.

The Wallet of a player then represents the collection of license a player owns. This is not for example an inventory as we might see in an RPG, but could indicate what your game should populate such an inventory with.
{% endhint %}

## Use Cases

### List the user's wallets

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/api/wallets#list" %}

{% hint style="warning" %}
This is an asynchronous operation and must be executed as a co-routine within Unity
{% endhint %}

```csharp
StartCoroutine(API.Wallets.List((requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.Count + " wallets");
        }
    }));
```

The List method of the Wallet API takes a single parameter, which is its "callback"

A callback is a method that will be called when the operation has completed. In the example above we used expression to define an anonymous method; you could also have provided it with a method defined in the calling class that takes a parameter of type `ListWalletResult` for example

```csharp
public void HandleWalletResults(ListWalletResult requestState)
{
    if (!requestState.hasError)
    {
        Debug.Log("Found " + requestState.result.Count + " wallets");
    }
}
```

### Check for tokens

In this case we need to know the wallet we want to read first. Lets assume we want to read all of the wallets the user owns to check for all owned tokens

{% hint style="info" %}
Example Coming Soon!
{% endhint %}
