---
description: Get a peek at what's new and upcoming to Steamworks
---

# 🆕 What's New

<figure><img src="../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

Heathen's Steamworks is under constant development and improvement. It is available for Unity and Godot game engines and can be licensed from the Unity Asset Store or directly from Heathen by becoming a GitHub Sponsor (recommended).&#x20;

This page will give you a sneak peak at what's coming to each platform and help you understand what to expect from the Unity Asset Store version.

{% hint style="info" %}
The Unity Asset Store (UAS) version is necessary behind the latest version. In particular when working on "Major" changes UAS can be multiple months behind the latest due to a myriad of complexities and limitations with the Unity Asset Store and that distribution pipeline.\
\
This documentation is keep up to date with the latest and so this page can help you understand what features are coming to UAS but are currently only available to GitHub Sponsors.\
\
We will only post about new features here when they hit the GitHub Source Repo for Unity here.

\
Godot source is derived from Unity source so will be slightly behind its self.
{% endhint %}

## Godot Engine

:tada: Steamworks Complete is coming to Godot!

Steamworks Foundation v1.0 was recently completed and is available on GitHub. Updates are in the works to it and the Unity Engine to create a more unified code base. in particular the new AchievementData, ItemData, LeaderboardData, LobbyData and similar \`Data\` objects are forth coming. These will compensate for Godot's lack of ScriptableObjects in many cases and creates a common engine agnostic layer for most tools and systems.

On release Godot will contain all API and Objects defined for Steamworks Complete. Samples will be added over time to create a library similar to that seen in Unity.

## Unity Engine

### Data Layer

A new \`Data\` object layer is being created to act as a mid level abstraction of Steam API and provide for a common code base between Godot and Unity. These \`Data\` objects such as UserData, LobbyData, AchievementData and more will have engine specific features such as returning avatars, icons, etc. in the engine's native "texture" format but will have identical functionality between the two engines.

Data objects are simple structs that are implicitly convertible with the underlying native data type for example one can convert a ulong value to a [UserData ](objects/user-data.md)object

```csharp
UserData myFriend = 123456789987;
```

Assuming that ulong value is a valid ID for your friend UserData gives you access to all relevant data for that user

```csharp
Debug.Log($"Hello {myFriend.Nickname} its good to see you!");
```

Data objects provide simple static \`Get\` methods for those of you uncomfortable with implicit conversion.

```csharp
UserData myFriend = UserData.Get(123456789987);
```

In most cases we have Get overloads for multiple valid types for example the UserData object can read a ulong value and interpret it as a CSteamID and it can read an int value and interpret it as an account / friend ID.

The addition of the Data Layer brings a new level of utility to the Steamworks integration which is of great use for scripters and programmers but also simplifies work for designers and UI/UX teams. Scriptable Objects will still be present and have all the functionality they do now they will simply be changed to work with the new Data Layer.

### UI Controls & Prefabs

We are developing production ready prefabs and UI controls to satisfy the most common use cases noted by our community. These include Leaderboard Display Lists, Part Lobby Control, Quick Match Lobby Control, Friend Lists, Invite Dropdowns and much more. The intent is that a developer should be able to use prefabs to yield a functional "out of the box" integration leveraging every major feature of Steam API with zero custom code.

This however doesn't mean you wont need to understand some basic scripting. While these prefabs will solve for the most common use cases most games will have some degree of bespoke logic and will require you to create some custom controls. These new prefabs though will allow you to prototype faster and solve for low importance features with a drag and drop solution as well as of course providing a solid working example of how to get started with your bespoke UI.&#x20;

### Sample Scenes

We are revamping all of our sample scenes. The current/previous design approach was to provide bare bones examples with custom scripts demonstrating each major feature set's core functionality. While this worked well for some it wasn't enough for many.

The new approach is to add "practical use case" sample scenes, that is functional examples of each features use as it might appear in game. These new practical use case scenes will leverage the new UI Controls heavily but will also include examples of creating bespoke UI controls. The objective is to give a more detailed working example of a production ready implementation of Steamworks.&#x20;

When coupled with the new UI Controls and Prefabs this will allow developers to Do More with less code.&#x20;

{% hint style="danger" %}
We are **NOT** advocates of code free game development.\
We believe you will and should still create bespoke / custom game logic.\
\
The purpose of these more elaborate scenes and prefabs are to help guide you in creating your own and to provide suitable options for rapid prototyping. We **DO NOT** recommend you use them un-altered in a production game if only for the "asset flip" issue.
{% endhint %}

