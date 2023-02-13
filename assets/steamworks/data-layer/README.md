---
description: Simple structs, powerful features!
---

# 🧪 Data Layer

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

A mid level abstraction of Steam API and a common code base between Godot and Unity. These \`Data\` objects such as UserData, LobbyData, AchievementData and more have engine specific features such as returning avatars, icons, etc. in the engine's native "texture" format but will have identical functionality between the two engines.

Data objects are simple structs that are implicitly convertible with the underlying native data type for example one can convert a ulong value to a [UserData ](user-data.md)object

```csharp
UserData myFriend = 123456789987;
```

Data objects are also implictly convertable with Steam's native types for each artifact for example

```csharp
CSteamID friendNativeId = new CSteamID(123456789987);
UserData myFriend = friendNativeId;
```

This implicit conversion means  that you can use Heathen's Data layer interchangeably with any other system for either the underlying primitive type or the Steam API native type without needing to manually convert your self.

This also means you can easily get all of the core features of each artifact quickly and easily and with no need of reference objects or use of APIs ours or raw Steam API.

```csharp
Debug.Log($"Hello {myFriend.Nickname} its good to see you!");
```

Data objects provide simple static \`Get\` methods for those of you uncomfortable with implicit conversion.

```csharp
UserData myFriend = UserData.Get(123456789987);
```

In most cases we have Get overloads for multiple valid types for example the UserData object can read a ulong value and interpret it as a CSteamID and it can read an int value and interpret it as an account / friend ID.

The addition of the Data Layer brings a new level of utility to the Steamworks integration which is of great use for scripters and programmers but also simplifies work for designers and UI/UX teams. Scriptable Objects will still be present and have all the functionality they do now they will simply be changed to work with the new Data Layer.
