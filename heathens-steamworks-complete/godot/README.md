---
cover: ../../.gitbook/assets/Godot Banner@4x-100.jpg
coverY: 0
---

# 🚧 Godot

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The articles within are specific to Godot and include the engine specific tools and systems unique to the Godot version of the package.&#x20;

The Heathen [APIs](../unity/api/) and [Objects](../unity/objects/) being native C# are \*\***nearly\*\*** identical between Unity and Godot with the only difference being the use of each engines native structures ...&#x20;

for example&#x20;

in Godot:

```csharp
public void LoadAvatar(Action<Image> callback)
```

in Unity:

```csharp
public void LoadAvatar(Action<Texture2D> callback)
```

{% hint style="info" %}
At current only the Foundation version of Heathen's Steamworks is available for Godot. We are working on porting the full Steamworks Complete asset however this will take time.
{% endhint %}

## Foundation

{% embed url="https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Godot" %}
Godot Project Template
{% endembed %}

Steamworks Foundation is a freely available "lite" version of Heathen's Steamworks Complete. It is an extension of Steamworks.NET and so does provide access to every aspect of the Steam API. The differences between Foundation and Complete are the additional tools and systems Heathen has created ontop of Steamworks.NET.

The Foundation version contains the basics such as

### Steamworks Behaviour

This initializes the Steam API and handles configuration and running callback update.

### [API.Friends](../unity/api/friends.client.md)

This is an extension of the SteamFriends API end point and greatly simplifies working with friends, UserData and related tasks

### [API.Overlay](../unity/api/overlay.client.md)

This is an extension of several parts of Steam API simplifies handling of overlay features and reacting to invite events

### [API.Utilities](../unity/api/utilities.client.md)

A set of misc tools from Valve useful&#x20;

### [UserData](../unity/sample-scenes/user-data.md)

A helpful tool for working with Steam user data providing simple access to features like Rich Presence, Nickname, Avatar images and more!
