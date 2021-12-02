---
description: HeathenEngineering.BGSDK.API.Tokens
---

# Tokens

```csharp
HeathenEngineering.BGSDK.API.Server.Tokens
```

A wrapper around token management features.

## Overview

{% hint style="warning" %}
These methods can only be called from a server build.
{% endhint %}

The Token API is primarily used during dev time, that is most of the actions against a token type or "template" will be performed in the Unity Editor while creating your game/app, and can be done through the editor tools as described in the [Getting Started](../learning/getting-started.md) article.&#x20;

{% content-ref url="../learning/getting-started.md" %}
[getting-started.md](../learning/getting-started.md)
{% endcontent-ref %}

{% hint style="info" %}
The only relevant Token function to be used during run time is the "Get" operation, which can be executed from the raw api such as:&#x20;

```csharp
API.Server.Tokens.GetTokens(token, resultAction);
```

or can be called on the Token object itself

```csharp
myToken.Get(resultAction);
```

This of course assumes that `mytoken` is a reference to a Token ScriptableObject such as you defined in your BGSDK Settings object.
{% endhint %}

## Features

### List Contracts

```csharp
public static IEnumerator ListContracts(Action<ListContractsResult> callback);
```

List the available contracts configured for the app.&#x20;

In most cases this will not be needed at run time as you should already have all contracts used by your app defined as Contract objects in your BGSDK Settings.

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Tokens.ListContracts((requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.Count + " contracts");
        }
    }));
```

### Get Contract

```csharp
public static IEnumerator GetContract(Contract contract, 
    Action<ContractResult> callback);
```

Get data about a target contract.

In most cases this will not be needed at run time as you should already have all contracts and all relevant contract data used by your app defined in your Contract objects in your BGSDK Settings.

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Tokens.GetContract(contract, (requestState) =>
    {
        if (!requestState.hasError && requestState.result.HasValue)
        {
            Debug.Log("Found " + requestState.result.Value.name + " contract data");
        }
    }));
```

### List Token Types

```csharp
public static IEnumerator ListTokenTypes(Contract contract, 
    Action<ListTokenTypesResult> callback);
```

Gets a list of available tokens in a given contract.

In most cases this will not be needed at run time as you should already have all tokens and all relevant token data used by your app defined in your Token objects in your BGSDK Settings.

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Tokens.ListTokenTypes(contract, (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.Count + " token types");
        }
    }));
```

### Get Token Type

```csharp
public static IEnumerator GetTokenType(Contract contract, 
    string tokenId,
    Action<ContractResult> callback);
```

Get data about a target token.

In most cases this will not be needed at run time as you should already have all contracts and all relevant token data used by your app defined in your Token objects in your BGSDK Settings.

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Tokens.GetTokenType(contract, id, (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.name + " token data");
        }
    }));
```

### Get Tokens

```csharp
public static IEnumerator GetTokens(Token token,
    Action<Token.ResultList> callback);
```

Get the tokens of the same type the user has.

{% embed url="https://docs.arkane.network/api/api-products/nft-api/retrieve-nfts-by-template" %}

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Server.Tokens.GetTokens(token, (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.Count + " tokens");
        }
    }));
```

## Privileged Features

{% hint style="danger" %}
These are features that are only available in the editor or server builds and are for testing purposes only!

These features will not compile for client builds.
{% endhint %}

### Mint Non Fungible Token

```csharp
public static IEnumerator Privileged.MintNonFungibleToken(Token token,
    string[] destinations,
    Action<BGSDKBaseResult> callback);
```

Creates an instance of this token on the destinations indicated. Note the destinations are wallet addresses.

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Privileged.MintNonFungibleToken(token, 
    destinations,
    (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Tokens created");
        }
    }));
```

### Mint Fungible Token

```csharp
public static IEnumerator Privileged.MintFungibleToken(Token token,
    int[] amounts,
    string[] destinations,
    Action<BGSDKBaseResult> callback);
```

Creates an amount of this token on the destinations indicated. Note the destinations are wallet addresses.

{% embed url="https://docs.arkane.network/api/api-products/nft-api/mint-fungible-nft" %}

#### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.Privileged.MintFungibleToken(token, 
    amounts,
    destinations,
    (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Tokens created");
        }
    }));
```
