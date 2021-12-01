---
description: HeathenEngineering.BGSDK.API.Wallets
---

# Wallets

```csharp
HeathenEngineering.BGSDK.API.Server.Tokens
```

A wrapper around token management features.

{% embed url="https://docs.venly.io/api/api-products/wallet-api" %}

## Overview

Wallets are the primary means to interact with the Blockchain assets from within your game/app at run time. The typical use case is to fetch the list of wallets owned by the current user, and use these during the execution of your game or app to fetch specifics about the items the current user owns.

{% hint style="info" %}
Note that "minting" or creating new items (tokens) is a secure operation that cannot be performed from the game/app client. That is the program the player is running cannot itself create a new token and add it to the users wallet.&#x20;

Instead you will need to use a trusted system such as a Web Server or Live Operations provider to perform these trusted operations against the Arkane Web API.

The purpose of the BGSDK integration in Unity is to simplify the use of these items in game e.g. to easily query what items a user has, and relate that to objects in Unity for gameplay/app execution purposes.
{% endhint %}

## Features

### Create

{% hint style="warning" %}
This methods should only be called from a server build.
{% endhint %}

```csharp
public static IEnumerator Create(string pincode, 
    string identifier, 
    string description, 
    SecretType chain, 
    Type type, 
    Action<ListWalletResult> callback);
```

Creates a new White Label Wallet for the indicated user. This method is capable of creating recoverable or unrecoverable wallets as defined by Arkane.

#### Parameters

| Type                      | Name        | Note                                                                                       |
| ------------------------- | ----------- | ------------------------------------------------------------------------------------------ |
| string                    | pincode     | <p>Must be a non-empty value</p><p>The pin that will encrypt and decrypt the wallet</p>    |
| string                    | identifier  | <p>Can be null or empty</p><p>An identifier that can be used to query or group wallets</p> |
| string                    | description | <p>Can be null or empty</p><p>A description to describe the wallet</p>                     |
| Wallet.SecretType         | chain       | The blockchain on which to create the wallet                                               |
| Wallet.Type               | type        | Define if the wallet is recoverable or unrecoverable                                       |
| Action\<ListWalletResult> | callback    | A method invoked on completion of the process and containing the results of the execution. |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.Create(pincode,
    identifier,
    description,
    Wallet.SecretType.MATIC,
    Wallet.Type.WHITE_LABEL,
    (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Created wallet " + requestState.result[0].address);
        }
    }));
```

### List

{% hint style="warning" %}
This methods should only be called from a server build.
{% endhint %}

```csharp
public static IEnumerator List(Action<ListWalletResult> callback);
```

Returns the list of wallets owned by the authenticated user if any.

#### Parameters

| Type                      | Name     | Note                                                                                       |
| ------------------------- | -------- | ------------------------------------------------------------------------------------------ |
| Action\<ListWalletResult> | callback | A method invoked on completion of the process and containing the results of the execution. |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.List((requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.Count + " wallets");
        }
    }));
```

### Get

{% hint style="info" %}
This method is useful on both client and server builds.
{% endhint %}

```csharp
public static IEnumerator Get(string walletId,
    Action<ListWalletResult> callback);
```

Gets a specific or group of wallets from the user queried by ID.

#### Parameters

| Type                      | Name     | Note                                                                                        |
| ------------------------- | -------- | ------------------------------------------------------------------------------------------- |
| string                    | walletId | <p>Must be a non-empty value</p><p>The identifier to fetch a single or group of wallets</p> |
| Action\<ListWalletResult> | callback | A method invoked on completion of the process and containing the results of the execution.  |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.Get(walletId,
    (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.Count + " wallets");
        }
    }));
```

### Balance

{% hint style="info" %}
This method is useful on both client and server builds
{% endhint %}

{% hint style="info" %}
You will notice two "balance" members in the Wallet API

```csharp
public static IEnumerator Balance(...);
```

and

```csharp
public static IEnumerator TokenBalance(...);
```

The`Balance`option will return a native balance e.g. the balance of tokens native to that chain as well as the gas balance, and raw balance values.

The`TokenBalance`option will return the list of tokens supported by BGSDK found in this wallet e.g. indicating the token address, type, etc.
{% endhint %}

```csharp
public static IEnumerator NativeBalance(string walletId,
    Action<BalanceResult> callback);
```

Gets the balance of non fungible tokens in the users wallet.

#### Parameters

| Type                   | Name     | Note                                                                                        |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------- |
| string                 | walletId | <p>Must be a non-empty value</p><p>The identifier to fetch a single or group of wallets</p> |
| Action\<BalanceResult> | callback | A method invoked on completion of the process and containing the results of the execution.  |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.NativeBalance(walletId,
    (requestState) =>
    {
        if (!requestState.hasError && requestState.success)
        {
            Debug.Log("Found " + requestState.result.Count + " token types");
        }
    }));
```

### Token Balance

{% hint style="info" %}
This method is useful on both client and server builds
{% endhint %}

{% hint style="info" %}
You will notice two "balance" members in the Wallet API

```csharp
public static IEnumerator Balance(...);
```

and

```csharp
public static IEnumerator TokenBalance(...);
```

The`Balance`option will return a native balance e.g. the balance of tokens native to that chain as well as the gas balance, and raw balance values.

The`TokenBalance`option will return the list of tokens supported by BGSDK found in this wallet e.g. indicating the token address, type, etc.
{% endhint %}

```csharp
public static IEnumerator TokenBalance(string walletId,
    Action<TokenBalanceResult> callback);
```

Gets the balance of tokens in the users wallet.

#### Parameters

| Type                        | Name     | Note                                                                                        |
| --------------------------- | -------- | ------------------------------------------------------------------------------------------- |
| string                      | walletId | <p>Must be a non-empty value</p><p>The identifier to fetch a single or group of wallets</p> |
| Action\<TokenBalanceResult> | callback | A method invoked on completion of the process and containing the results of the execution.  |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.TokeBalance(walletId,
    (requestState) =>
    {
        if (!requestState.hasError && requestState.success)
        {
            Debug.Log("Found " + requestState.result.Count + " token types");
        }
    }));
```

### Specific Token Balance

{% hint style="info" %}
This method is useful on both client and server builds
{% endhint %}

```csharp
public static IEnumerator SpecificTokenBalance(string walletId,
    string tokenAddress,
    Action<TokenBalanceResult> callback);
```

Gets the balance of non fungible tokens in the users wallet.

#### Parameters

| Type                        | Name         | Note                                                                                        |
| --------------------------- | ------------ | ------------------------------------------------------------------------------------------- |
| string                      | walletId     | <p>Must be a non-empty value</p><p>The identifier to fetch a single or group of wallets</p> |
| string                      | tokenAddress | <p>Must be a non-empty value</p><p>The address of the token to fetch data for</p>           |
| Action\<TokenBalanceResult> | callback     | A method invoked on completion of the process and containing the results of the execution.  |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.NFTs(walletId,
    (requestState) =>
    {
        if (!requestState.hasError && requestState.success)
        {
            Debug.Log("Found " + requestState.result.Count + " token types");
        }
    }));
```

### NFTs

{% hint style="info" %}
This method is useful on both client and server builds
{% endhint %}

```csharp
public static IEnumerator NFTs(string walletId,
    List<string> optionalContractAddresses,
    Action<NFTBalanceResult> callback);
```

Gets the balance of non fungible tokens in the users wallet.

{% embed url="https://docs.arkane.network/api/api-products/wallet-api/retrieve-token-balances" %}

#### Parameters

| Type                      | Name                       | Note                                                                                        |
| ------------------------- | -------------------------- | ------------------------------------------------------------------------------------------- |
| string                    | walletId                   | <p>Must be a non-empty value</p><p>The identifier to fetch a single or group of wallets</p> |
| List\<string>             | opttionalContractAddresses | When set, the result will only contain tokens of these NFT contract addresses.              |
| Action\<NFTBalanceResult> | callback                   | A method invoked on completion of the process and containing the results of the execution.  |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.NFTs(walletId,
    (requestState) =>
    {
        if (!requestState.hasError && requestState.success)
        {
            Debug.Log("Found " + requestState.result.Count + " token types");
        }
    }));
```

### Update Pincode

{% hint style="warning" %}
This methods should only be called from a trusted Web Server.
{% endhint %}

```csharp
public static IEnumerator UpdatePincode(string walletId,
    string currentPincode,
    string newPincode,
    Action<ListWalletResult> callback);
```

Gets a specific or group of wallets from the user queried by ID.

{% embed url="https://docs.arkane.network/api/api-products/wallet-api/update-pin" %}

#### Parameters

| Type                      | Name           | Note                                                                                        |
| ------------------------- | -------------- | ------------------------------------------------------------------------------------------- |
| string                    | walletId       | <p>Must be a non-empty value</p><p>The identifier to fetch a single or group of wallets</p> |
| string                    | currentPincode | <p>Must be a non-empty value</p><p>The current pincode for the wallet</p>                   |
| string                    | newPincode     | <p>Must be a non-empty value</p><p>The new pincode to be applied to the wallet</p>          |
| Action\<ListWalletResult> | callback       | A method invoked on completion of the process and containing the results of the execution.  |

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Wallets.UpdatePincode(walletId,
    currentPincode,
    newPincode,
    (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Updated pin on wallet " + requestState.result[0].address);
        }
    }));
```

###
