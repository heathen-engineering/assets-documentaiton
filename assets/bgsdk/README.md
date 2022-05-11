---
description: >-
  Heathen Engineering's BGSDK Foundation allows you to manage in-game items as
  blockchain assets. It is a complete wrapper around Venly's Web API.
---

# Blockchain Game SDK

{% embed url="https://discord.gg/6X3xrRc" %}

## Introduction

{% hint style="info" %}
"Minting" or creating new items (tokens) is a secure operation that cannot be performed from the game/app client.&#x20;

That is to say, the program that the player is running \***cannot**\* its self create a new token and add it to the users wallet.&#x20;

Instead you will need to use a trusted system such as a Web Server or Live Operations provider to perform these trusted operations against the Venly Web API.

The purpose of the BGSDK kit at runtime in Unity is to simplify the use of these items in game e.g. to easily query what items a user has and relate that to objects in Unity for gameplay/app execution purposes.

BGSDK kit at dev time, that is within the Unity Editor can be used to perform "trusted" operations such as minting tokens, creating new token and contract types, etc. These operations are made available for testing purposes only and cannot be ran during run time.
{% endhint %}

Heathen Engineering's BGSDK Foundation allows you to manage in-game items as blockchain assets. It is a complete wrapper around [Venly](https://www.venly.io)'s Web API with regards to client safe operations. The tool simplifies integration with Arkane API exposing all relevant features and functions to C# classes and includes Editor extensions to aid in design and deployment of Contracts and Tokens.

{% embed url="https://docs.venly.io/api/" %}

### Playable Demo

{% embed url="https://simmer.io/@Loden/bgsdk-foundation" %}
Playable Demo using the BGSDK Foundation
{% endembed %}

## Requirements

Please note that you will need to register for an account with [Venly Network](https://www.venly.io) to receive the required Client ID and Secret used by the kit to connect to the [Venly Network](https://www.venly.io) backend. This must be acquired from [Venly Network](https://www.venly.io) directly.

## Features

The following tables map the Venly Web API functions to corresponding functions in Unity.

### User API

{% hint style="warning" %}
2021-10-05

The Venly authentication methods are temporarily deprecated as per Venly request. If you have any questions or need more support around authentication through the Venly APIs please contact Venly.
{% endhint %}

For the Web API the features are covered under the "[How to authenticate](https://docs.venly.io/api/authentication/authentication)" Heathen's wrapper around the web API exposes them as shown below.

{% hint style="info" %}
Once authenticated the system will maintain the authentication token in memory. You should not need to worry about authenticating the user again after that initial authentication is handled.
{% endhint %}

| Unity SDK                                                                        | Use                                                 |
| -------------------------------------------------------------------------------- | --------------------------------------------------- |
| [User.GetProfile](api/user.md#get-profile)                                       | Fetches information about the authenticated user    |
| [User.Login\_3rdPartyAuthentication](api/user.md#login-3rd-party-authentication) | Takes access token data in from an outside source   |
| [User.Login\_Facebook](api/user.md#login-facebook)                               | Exchanges a facebook token to authenticate the user |

### Wallet API

Wallet API features are the core of what you will be using at run time in your game/app. Heathen methods are all part of static classes which assume authentication has already been handled.&#x20;

| Web API                                                                                                      | Unity SDK                                                                                                         |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| [Create wallet](https://docs.venly.io/api/api-products/wallet-api/create-wallet)                             | [Wallets.Create](https://kb.heathenengineering.com/assets/bgsdk/api/wallets#create)                               |
| [Update wallet PIN](https://docs.venly.io/api/api-products/wallet-api/update-pin)                            | [Wallets.UpdatePincode](api/wallets.md#update-pincode)                                                            |
| [Retrieve a wallet](https://docs.venly.io/api/api-products/wallet-api/get-wallet)                            | [Wallets.Git](api/wallets.md#get)                                                                                 |
| [Retrieve all wallets](https://docs.venly.io/api/api-products/wallet-api/untitled)                           | [Wallets.List](api/wallets.md#list)                                                                               |
| [Retrieve wallet balance](https://docs.venly.io/api/api-products/wallet-api/retrieve-wallet-balance)         | [Wallets.Balance](https://kb.heathenengineering.com/assets/bgsdk/api/wallets#balance)                             |
| [Retrieve token balance](https://docs.venly.io/api/api-products/wallet-api/retrieve-token-balances)          | [Wallets.TokenBalance](https://kb.heathenengineering.com/assets/bgsdk/api/wallets#token-balance)                  |
| [Retrieve specific token balance](https://docs.venly.io/api/api-products/wallet-api/retrieve-token-balances) | [Wallets.SpecificTokenBalance](https://kb.heathenengineering.com/assets/bgsdk/api/wallets#specific-token-balance) |
| [Retrieve NFTs](https://docs.venly.io/api/api-products/wallet-api/retrieve-non-fungible-tokens)              | [Wallets.NFTs](https://kb.heathenengineering.com/assets/bgsdk/api/wallets#nfts)                                   |

### NFT API

Token management is a feature of Heathen's editor tools. Most of these features are wrapped up in the BGSDK Settings object and performed in bulk when you synchronize. As editor features they are not available at run time.

| Web API                    | Unity SDK                       |
| -------------------------- | ------------------------------- |
| Create Contract            | EditorUtilities.SyncSettings    |
| Retrieve Contract          | EditorUtilities.SyncSettings    |
| Retrieve all contracts     | EditorUtilities.SyncSettings    |
| Create NFT template        | EditorUtilities.SyncSettings    |
| Retrieve NFT template      | EditorUtilities.SyncSettings    |
| Retrieve all NFT templates | EditorUtilities.SyncSettings    |
| Retrieve NFT metadata      | Coming Soon                     |
| Mint NFT                   | Privileged.MintNonFungibleToken |
| Mint fungible token        | Privileged.MintFungibleToken    |
| Retrieve NFTs by template  | EditorUtilities.SyncSettings    |
