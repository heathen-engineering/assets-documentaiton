# NFTs in Game

{% hint style="danger" %}
This article is the openion of its author and is **Not Legal advice**
{% endhint %}

## Introduction

A rather huge problem with the Blockchain hype and the craze around NFT (Non-Fungible Tokens) is that it hasn't been made particularly clear how these are used in game or really anywhere.

While others may have different opinions from a game developer's point of view its best to think of an NFT as a license. If your old enough to remember when games came in a box you may remember "CD Keys" these where unique identifiers that represented your license to play the game and had to be entered to install the game on your machine. A NFT is best used as a "CD Key" that is as a means to know who has the licensing rights to consume a given bit of content.

A good example of a good use for blockchain technology in game is as game license and or DLC license. This could allow players to buy used copies, trade games with there friends, etc. while insuring a secure way for you to know the user has a valid license and to insure you get a cut of any re-sale if you so wanted.

### Ownership

Ownership is a concept that has become confused as of late and I really don't understand why its confusing.

When you buy a movie, picture, song, book, game or any other such thing you are not buying the rights to the property you are buying a consumer license to a copy of the property. You cannot duplicate it and in some cases you cannot transfer the license depending on the terms the license may also be revokable or restrict your use in other ways.&#x20;

Why all of a sudden there is confusion about the concept of "license" I am not sure. This is not new concept and has always been the case well before games where even a thing.

With regards to NFTs it is our opinion that you should make it clear that this is no different than buying a skin in Fortnight, a game on Steam, a Mount in World of Warcraft, etc. Digital goods exchanged for real money even between players out side of the game world is nothing new to the game industry.&#x20;

### Content

While it is possible to embed your content in the NFT its self there is no useful reason to do so. Considering your NFT represents a license to some media and like any media that media may need to be updated, adapted, etc. over time its our opinion that its best to not store any such data in the NFT its self rather use it as a simple "key" to denote access to some content in your game world or a license to play the game or DLC, etc.

## Why

So if you read the above at all you may be wondering ....

If NFT is no different than Steam Inventory, DLC, MTX items such as Fortnight skins, WoW mounts, etc.&#x20;

and

If NFTs are basically comparable to Inventory items or at best DLC licenses why bother with NFT at all?

In most of the cases we hear pitched around; you shouldn't be considering NFT for that. Minting and transferring NFTs has a cost and complexity that is very often higher than other more traditional solutions for most in-game use cases you may be thinking of.

There are however strong use cases where Blockchain technology brings features and capabilities that aren't possible or perhaps are but are not practical without it. The example of licensing your game as a NFT and or its DLC as NFTs thus enabling player's to sale old games, buy used games, etc. that is a unique use that other solutions could do but not well.

The notion of cross game and cross game developer items is another interesting notion. It can and has be done with other solutions but may be made more practical via blockchain technology as most inventory systems are designed to restrict to a game or at least a publisher.

## How

### Using Tokens and Wallets

Okay so your all ready to go, you have created your contracts and NFTs and you have assigned [white label wallets](white-label-wallets.md) to your users ... so how do you relate a token owned by a user to a token in your game client such that you know what content they have access to?

In short you read the user's wallet and check to see what token types they own and instance of.

so your first thing to do is ask for the NFTs housed in the wallet in question

```csharp
StartCoroutine(HeathenEngineering.BGSDK.API.Client.Wallets.NFTs(
                walletAddress, 
                SecretType.MATIC, 
                null, 
                HandleWalletResults));
```

This will invoke the HandleWalletResults method with the results when ready

```csharp
private void HandleWalletResults(NFTBalanceResult walletData)
{
    if (walletData.hasError)
    {
        Debug.LogError("Failed to read wallet contents: " + walletData.message);
    }
    else
    {
        foreach (var token in walletData.result)
        {
            //"token" is a reference the token you see in your BGSDK Settings
            //How you relate that to game content or features
            //depends on your game
        }
    }
}
```

Typically you would run this from your backend server so this is how your server knows what types of tokens this wallet contains. You could then send that information down to the client or use it to unlock features for that user etc.
