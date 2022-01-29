# Set User Avatar

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

A simple componenet meant to be attached to a UnityEngine.UI.RawImage

This can update the raw image with the indicated user's avatar and can optionally pull the local user's data on start up.

This will update if the linked user changes there avatar image.

## Definition

```csharp
[RequireComponent(typeof(UnityEngine.UI.RawImage))]
public class SetUserAvatar : MonoBehaviour
```

## Events

### Loaded

```csharp
public UnityEvent evtLoaded;
```

Occurs when the texture is loaded

The handler for this event would be as such

```csharp
public void HandleLoaded()
{
    //Avatar was loaded
}
```

## Fields and Attributes

### UseLocalUser

```csharp
private bool useLocalUser;
```

{% hint style="warning" %}
This can only be set in the Unity Editor and will be false for run time created componenets or if not set.
{% endhint %}

This causes the componenet to grab the local user's ID on startup.

### UserData

```csharp
public UserData UserData { get; set; }
```

This returns the UserData that this componenet is currently tracking. Setting this will cause this componenet to track the user you set to it and is the same as calling LoadAvatar;

## Methods

### Load Avatar

```csharp
public void LoadAvatar(UserData user);
```

```csharp
public void LoadAvatar(CSteamID user);
```

```csharp
public void LoadAvatar(ulong user);
```

Load the selected user's avatar image.
