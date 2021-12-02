# White Label Wallets

## Introduction

White Label Wallet is the core feature for integrating blockchain with your game or app. This is a standard blockchain wallet which can have a native balance and hold various NFTs. It is refered to as a White Label Wallet because its owned by your app not the user. This means your game can freely add and remove tokens from this wallet without needing involve the user.

You can think of a White Label Wallet like an inventory in a typical game. You could have a White Label Wallet for each player, character on a player's account, you could also have White Label Wallets to represent guild banks and so on.

## Creating a Wallet

{% embed url="https://docs.venly.io/api/api-products/wallet-api/create-wallet" %}

The act of creating a White Label Wallet is best done by your Trusted Web Server ... so for example if your game uses PlayFab you would write a Cloud Script to call the Venly Web API to create the wallet.

You can also use the BGSDK Server API to create the wallet from your game server. Note that its up to you to assoceate the wallet's ID with the user, character or whatever else this wallet is related to.

In general we dont recomend having the game server create wallets, its better if the game server stays focused on the game and you let your Web Server deal with the APIs.

### Server API

```csharp
StartCoroutine(Server.Wallets.Create(pincode,
    identifier,
    SecretType.MATIC,
    (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Created wallet " + requestState.result[0].address);
        }
    }));
```

## Reading Inventory / Wallet

The main thing your game will be doing with NFTs is seeing what NFTs the user owns and applying that information to your game. To do so you will need to know the address of the wallet you want to read from.

As noted in the above Creating a Wallet section you should have assoceated the wallet with your user's account, or character profile or whatever this wallet represents in your game's world. Once you have that address you can query it for NFTs with the Client API.

```csharp
StartCoroutine(Client.Wallets.NFTs(walletAddress,
    null,
    (walletItems) =>
    {
        if (!walletItems.hasError && walletItems.success)
        {
            foreach(var token in walletItems.result)
            {
                //DO WORK
            }
        }
    }));
```

## Tokens to GameObject

Based on the above two concepts you now have a wallet or "inventory" and you know what tokens are inside of it. Your next trick is to relate that information to something Unity can understand, this typically means mapping the token data found in a wallet to the Engine.Token type you defined in your Contracts.

Assuming the above Read Inventory / Wallet

```csharp
// ...
foreach(var token in walletItems result)
{
    var tokenType = token.TokenType;
}
// ...
```

tokenType is an [Engine.Token](../../artifacts/token.md), that scriptable object your BGSDK Settings object is managing for you. You now Know the user owns one of these and you can of course count how many they own if that is relivent for your game.
