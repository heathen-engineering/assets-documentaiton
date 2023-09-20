---
description: Get a peek at what's new and upcoming to Steamworks
---

# 🆕 What's New (V2 to V3)

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

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

### DOTs more DOTs

We have adjusted our architecture to no longer be dependent on MonoBehaviour component scripts. This means DOTs users can fully utilize all the power of Heathen's Steamworks Complete without needing to use any MonoBehaviour based components.

We did this by moving the initialization to the API.App static classes and we manage our own background thread which handles updating callbacks and input values for you. This also consaquently means it no longer matters if you destroy the Steamworks Behaviour component all it does any more is kick the process off.

#### So what?

So now you have more options with how you initialize and use Steam API.

1. You can use Steamworks Behaviour as you have traditionally been doing
2. You can use SteamSettings on its own by simply calling its [Init](unity/scriptable-objects/steam-settings/#init) method.
3. You can use Heathen's API by calling [App.Client.Initialize](unity-engine/api/app.client.md#initialize) or [App.Server.Initialize](unity-engine/api/app.server.md#initialize) as appropriate

This then means that

* Steamworks Behaviour while it can be used is no longer required e.g. no requirement for a GameObject + Component script
* Steamworks Behaviour is no longer fragile, e.g. you can destroy it and not break Steam API
* You can now force server initialization even in a client build ... just call [App.Server.Initialize](unity-engine/api/app.server.md#initialize) ... really don't recommend you do that but you can
* Steam API wont be blocked by you blocking the main update loop e.g. Pause, etc. We now run on our own background thread.
* It also means Godot and Unity will be even more alike, While Unity has the option of Steamworks Behaviour which is a uniquely Unity thing. That behaviour now is pretty hallow and just ends up calling the App APIs we created which are common across all versions.

### Data Layer

A new \`Data\` object layer is being created to act as a mid level abstraction of Steam API and provide for a common code base between Godot and Unity. These \`Data\` objects such as UserData, LobbyData, AchievementData and more will have engine specific features such as returning avatars, icons, etc. in the engine's native "texture" format but will have identical functionality between the two engines.

Data objects are simple structs that are implicitly convertible with the underlying native data type for example one can convert a ulong value to a [UserData ](unity-engine/data-layer/user-data.md)object

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

## Major Update F.A.Q

### Will all my code break?

No ... but you will need to update a few things&#x20;

By in large these changes will not have a syntax change so wont break your current logic. In some cases low level names are changing ... Lobby for example is now called LobbyData in order to match the naming convention of other "data" layer objects. This will result in a compiler error for people using Lobby directly but should be trivial to resolve ... in most cases you should be able to right click and take the "Suggested Solution" in your IDE to fix any such cases.

We have also added a new "Data" layer that sits between the Scriptable Objects and the underlying API. This adds more flexability and reduces the bespoke code between objects improving stability and maintainability but does mean the "name" of Stats, Achievements and Leaderboards at least will need to be re-applied in your Steam Settings object

### Will GitHub Sponsors have to pay more?

No

GitHub Sponsors at the $15 have access to our source repository so not only will that price not be effects but you will see these changes happen as they are made and become stable. You are working on the same source repo that our own internal projects work on.

### Will Unity Asset Store users have to pay again and if so how much?

Newer users will get "grandfathered in" with a free upgrade, all other users will get a steep discount on the upgrade.

As to how much that isn't known yet, pricing is assessed based on the asset and state of the market at time of publish. We do not rase prices lightly and will avoid an increase to price if that is viable.

As to the Unity Asset Store "Major Update" and "Upgrade Discount" features:

Unity Asset Store has a feature called "Major Update" where we can give the update to user's who recently purchased the new version for free ... recent is a variable term with Unity but last time we managed 90 days. For other users who purchased V2 some time older than that we can and will offer a big discount for the first several months, that discount will slowly fall off.

### Can Unity Asset Store users get the GitHub download?

Yes

Anyone can join the GitHub Sponsor program, all sponsors at the $15 monthly tier get instant access to our source repository along with the Heathen standard license which is theirs to keep.

You can thus sub for 15 USD, download what you like, cancel right away if you want and go about your business. If you ever need or want another update resub and get another month of live updates.

GitHub Sponsor is the best way to Do More with Heathen rather or not you own some or all of our assets through Unity Asset Store as well. GitHub Sponsor program is \*\***much**\*\* more than just a way to get our assets. It empowers this Knowledge Base, it fuels on going development, new tools, live support and management of the growing community and a lot more.

Learn more about [what the GitHub Sponsor program is here!](../../become-a-sponsor/)
