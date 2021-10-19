---
description: Blockchain Game SDK assets for the Unity game engine from Heathen Engineering
---

# Artifacts

## Introduction

The BGSDK manages the Venly Web API via 3 main artifact types. An artifact is simply a Scriptable Object with specific functionality for the type of artifact

### BGSDK Settings

```csharp
public class BGSDKSettings : ScriptableObject;
```

This is the core artifact which contains references to all other artifacts and provides the point of entry look ups and editor actions. You can use the BGSDK Settings object to locate any other artifact.

![](<../../../.gitbook/assets/image (60).png>)

In addition to artifact look up, it is the BGSDKSettings object that houses the identity for the authenticated user, the URL references to the Web API's end points and the client ID which is how the API knows what account actions and queries should operate against.

Its in the BGSDK Settings inspector window that you would define new contracts and tokens, and during development time you can use this editor to publish these changes to the Venly backend.

![](<../../../.gitbook/assets/image (50).png>)

### Contract

```csharp
public class Contract : ScriptableObject;
```

This object represents a contract on the blockchain and stores a reference to the Tokens defined within it

![](<../../../.gitbook/assets/image (51).png>)

You would create a new contract by clicking the "Add Button" option on the BGSDK Settings

![](<../../../.gitbook/assets/image (52).png>)

Doing so will create a new Contract object in your asset database next to your settings object, and then list that object in your Model list on the settings.&#x20;

You can remove a contract from the system by clicking the red "-" button beside the contract in the Model listing on the BGSDK Settings object.

![](<../../../.gitbook/assets/image (55).png>)

Doing so will delete the contract and all tokens related to it from your asset folder.&#x20;

{% hint style="warning" %}
Deleting an object from Unity does not delete it from the Venly backend. If you have already published a contract and or token then it is on the backend and cannot be removed or edited.
{% endhint %}

{% hint style="info" %}
You can move the contract and token objects anywhere you like within your Unity Asset folder. Moving objects will not adversely effect the settings object.
{% endhint %}

### Token

```csharp
public class Token : ScriptableObject
```

This object represents a token type and is stored within the contract artifact.&#x20;

![](<../../../.gitbook/assets/image (53).png>)

You would create a new token by clicking the "+" button beside the contract in the Model listing on your BGSDK Settings object.

![](<../../../.gitbook/assets/image (54).png>)

Doing so will create a new Token object in your asset folder next to your BGSDK Settings object and will list it on the Contract it was created for, and display that listing in the Model tab of the BGSDK Settings object.

You would delete a token by clicking the "-" button beside the token you wish to remove in the Model listing on your BGSDK Settings object.

![](<../../../.gitbook/assets/image (56).png>)

Doing so will delete the token object from your Asset folder.

{% hint style="warning" %}
Deleting an object from Unity does not delete it from the Venly backend. If you have already published a contract and or token then it is on the backend and cannot be removed or edited.
{% endhint %}

