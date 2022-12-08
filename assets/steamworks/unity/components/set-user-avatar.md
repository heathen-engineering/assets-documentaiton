# Set User Avatar

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

A simple component meant to be attached to a UnityEngine.UI.RawImage

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
