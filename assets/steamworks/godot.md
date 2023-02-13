# 🤖 Godot Engine

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="./">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/concepts/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

The articles within are specific to Godot and include the engine specific tools and systems unique to the Godot version of the package.&#x20;

The Heathen [APIs](api/) and [Objects](objects/) being native C# are \*\***nearly\*\*** identical between Unity and Godot with the only difference being the use of each engines native structures ...&#x20;

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

### [API.Friends](api/friends.md)

This is an extension of the SteamFriends API end point and greatly simplifies working with friends, UserData and related tasks

### [API.Overlay](api/overlay.md)

This is an extension of several parts of Steam API simplifies handling of overlay features and reacting to invite events

### [API.Utilities](api/utilities.client.md)

A set of misc tools from Valve useful&#x20;

### [UserData](unity/samples/user-data.md)

A helpful tool for working with Steam user data providing simple access to features like Rich Presence, Nickname, Avatar images and more!
