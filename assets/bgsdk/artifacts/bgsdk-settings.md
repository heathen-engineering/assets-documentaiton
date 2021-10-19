---
description: Details and examples on the BGSDK Settings artifact
---

# BGSDK Settings

## Introduction

The BGSDK Settings object is the root of the BGSDK Unity asset and serves as the point of entry for most operations. The BGSDK also stores references to your blockchain datamodel, that is it stores references to your contracts and token types so that you do not need to query the Web API every time you want that data.

You must create a BGSDK Settings object in order to work with the Blockchain Game SDK in Unity.&#x20;

1. Right click in a folder on your "Project" tab in the Unity editor
2. Select "Create" > "Blockchain Game SDK" > "Settings" from the menu

You now have a new BGSDK Settings object which will be defaulted to use the staging API

{% hint style="info" %}
### Pro Tip

You can modify the API end points used by the system by switching the Unity Inspector into "Debug" mode. To do this click the ellipsis button in the upper right of the Inspector tab and select "Debug" from the options. This will cause the inspector to display the default editor exposing additional fields including the API end points.
{% endhint %}

![BGSDK Settings Inspector in "Debug" mode](<../../../.gitbook/assets/image (57).png>)

![BGSDK Settings Inspector in "Normal" mode](<../../../.gitbook/assets/image (58).png>)

### Application

The application tab of the settings inspector is used to configure your app. Here you would enter your Application ID, Client ID and Client Secret as provided to you by Venly.

![](<../../../.gitbook/assets/image (59).png>)

### API

The API tab can be used to toggle between staging and production.&#x20;

![](<../../../.gitbook/assets/image (61).png>)

### Model

The model tab is used to construct your blockchain data model, that is to define the contracts and tokens your game will work with.

![](<../../../.gitbook/assets/image (62).png>)

### Status Information

Along the bottom edge of the Inspector you will notice Status Information. This gives you tips as to the state of your data model based on common validation rules. These are simply meant to provide guidance.

![](<../../../.gitbook/assets/image (63).png>)

## Editor Examples

### Creating a Contract

{% hint style="warning" %}
Creating a contract in Unity does not automatically create the contract on the Venly backend (blockchain) you must "Synchronize" the settings object which will cause all new objects to be created on the blockchain, and any objects already on the blockchain to be created in Unity.

Be very careful when Synchronizing as once objects are published they cannot be edited or removed.
{% endhint %}

You can create a contract by simply clicking the "Add Contract" button located on the Model tab. This will create a new Contract artifact object in your asset folder and link it with the Settings object.

![](<../../../.gitbook/assets/image (52).png>)

### Creating a Token Type

{% hint style="warning" %}
Creating a contract in Unity does not automatically create the contract on the Venly backend (blockchain) you must "Synchronize" the settings object which will cause all new objects to be created on the blockchain and any objects already on the blockchain to be created in Unity.

Be very careful when Synchronizing as once objects are published, they cannot be edited or removed.
{% endhint %}

Once you have a contract defined in your Settings object you can create a Token type by clicking the "+" button beside the contract.

{% hint style="info" %}
You do not need to Synchronize the contract to the blockchain to create the token type in Unity.&#x20;

You should only Synchronize once you are sure that you are happy with the data model.
{% endhint %}

![](<../../../.gitbook/assets/image (54).png>)

### Remove a Contract

{% hint style="danger" %}
Removing a contract also removes its tokens. Be aware that this only removes the object from Unity you cannot "unpublish" an already published Contract and or Token type.
{% endhint %}

Contracts can be removed from the Settings object and your Asset folder by simply clicking the red "-" button beside the contract.

![](<../../../.gitbook/assets/image (55).png>)

### Remove a Token

{% hint style="danger" %}
removing a contract also removes its tokens. Be aware that this only removes the object from Unity you cannot "unpublish" an already published Contract and or Token type.
{% endhint %}

Tokens can be removed from the Settings object and your Asset folder by simply clicking the red "-" button beside the token.

![](<../../../.gitbook/assets/image (56).png>)

### Synchronize Changes

You can Synchronize changes with the blockchain by clicking the Synchronize button. Note that this will create contracts and tokens on the blockchain that are found in your settings object, and it will create contract and token artifacts in Unity that are found on the blockchain.

![](<../../../.gitbook/assets/image (64).png>)

## Code Examples

### Find a contract

{% hint style="info" %}
You can "lookup" a contract by its name, id or index however this is not as efficient as simply referencing the contract.

The entire reason Heathen created the Contract artifact is so you can reference it at development time and not need to perform in efficient run time look ups.
{% endhint %}

#### Reference&#x20;

```csharp
public class ExampleScript : MonoBehaviour
{
    public Contract myContract;
}
```

In the example above you can see we have simply created a public attribute on a script of type `Contract`With this done you can now drag and drop a contract from your asset folder onto this field in the Unity Inspector. This script can now access this contract's information via the `myContract` attribute e.g.&#x20;

```csharp
Debug.Log("The contract's ID is " + myContract.Id);
```

#### Look up by ID

```csharp
Contract contract = BGSDKSettings.current[contractId];
```

#### Look up by Index

```csharp
Contract contract = BGSDKSettings.current[contractIndex];
```

#### Look up by Name

```csharp
Contract contract = BGSDKSettings.current.FindContractByName("name");
```

### Find a token type

{% hint style="info" %}
You can "lookup" a token by its name, id or index however this is not as efficient as simply referencing the token.

The entire reason Heathen created the Token artifact is so you can reference it at development time and not need to perform in efficient run time look ups.
{% endhint %}

```csharp
public class ExampleScript : MonoBehaviour
{
    public Token myToken;
}
```

In the above you can see we have simply created a public attribute on a script of type `Token` . With this done you can now drag and drop a token from your asset folder onto this field in the Unity Inspector. This script can now access this token's information via the `myToken` attribute e.g.&#x20;

```csharp
Debug.Log("The token's ID is " + myToken.Id);
```

#### Look up by Id

This assumes you already have the contract

```csharp
Token token = contract[tokenId];
```

#### Look up by Index

This assumes you already have the contract

```csharp
Token token = contract[tokenIndex];
```

#### Look up by Name

This assumes you already have the contract

```csharp
Token token = contract.FindTokenByName("name");
```
