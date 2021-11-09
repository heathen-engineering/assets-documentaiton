# Set User Name

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

A simple componenet meant to be attached to a UnityEngine.UI.RawImage

This can update the raw image with the indicated user's avatar and can optionally pull the local user's data on start up.

### TMPro Set User Name

Set the user name for a target TextMesh Pro object

### uGUI Set User Name

Set the user name for a target uGUI Text object

## Definition

### Fields and Attributes

| Type                                      | Name         | Comments                               |
| ----------------------------------------- | ------------ | -------------------------------------- |
| <p>TextMeshProUGI</p><p>or</p><p>Text</p> | label        | The text object to put the name to     |
| bool                                      | useLocalUser | should we load the local user on start |



### Events

#### Loaded

Occurs when the texture is loaded

### Methods

```csharp
public void SetName(user);
```

Set the indicated user's name.
