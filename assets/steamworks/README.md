---
description: >-
  Heathen’s Steamworks is a set of tools, systems and editor extensions designed
  to make integrating Steam easier, faster, and more robust. Helping you Do More
  rather your a beginner or a pro.
cover: ../../.gitbook/assets/SteamMarketing Inventory hStretch.png
coverY: 17.4
---

# 🟦 Steamworks

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Do More

{% embed url="https://www.youtube.com/watch?v=6ujmZI1qUYI" %}

{% hint style="info" %}
[Become a Sponsor](../../become-a-sponsor/) and get all of our tools for 15$ its the best way to **Do More**!\


Available for Unity 3D and Godot (mono)\*\
\* [Foundation](https://github.com/heathen-engineering/SteamworksFoundation) is available for Godot now with Complete in development and coming soon.
{% endhint %}

We take the strength of Steamworks.NET, and the parody it has with the native APIs, and expand on that with engine centric tools, editor extensions and more!&#x20;

Heathen's Steamworks Complete is the best possible option for Unity & Godot (mono) developers looking to integrate with Steam API.&#x20;

## Battle Tested

{% embed url="https://store.steampowered.com/curator/42461073-Made-with-Heathen" %}

Trusted by [thousands of developers](https://discord.gg/6X3xrRc) we have been hard at work on this tool for more than a decade. [The Steam Curator link above](https://store.steampowered.com/curator/42461073-Made-with-Heathen) are just a few of the works our community have published covering many genre and demonstrating a wide range of examples from small passion projects to major commercial products.

## Built for You

Our tools are built in layers from powerful APIs and Frameworks up to code free solutions. No matter your need, skill level or discipline our tools can help you Do More!

{% hint style="success" %}
Whether you're new to Steam, or game development in general or maybe a seasoned veteran well capable with the Steam APIs, Heathen’s Steamworks can greatly accelerate your project and help you produce a more robust product that better leverages the services offered by Valve.&#x20;
{% endhint %}

From top to bottom each layer offers a level of simplicity and abstraction, you can mix and match as required to meet your project's and team's needs.

### Prefab & Tool Layer

We provide a range ready to use prefabs and simple script components that allow manny common requirements to be handled completely code free. All built on our easy to use Components Layer.

### Components Layer

We provide flexible and powerful tools in the form of component scripts and scriptable objects that simplify the use of every major Steam feature in editor with little or no code required. All built on our easy to use Data Layer.

### Data Layer

Our "data layer" is a set of structs and tools that simplify working with Steam's concepts and artifacts such as UserData, LeaderboardData, AchievementData and more. These greatly reduce the code and effort required to accomplish any task. All built on our robust API Layer.

### API Layer

Every end point and interface of Valve's Steam API has been expressed in a C# and Unity (or Godot) centric API. This means no need to mess with callbacks, manage operation queues cast and convert between various primitive and native types, etc.

The API Layer coupled with the Data Layer empowers programmers and engineers to work more efficiently and maintainable with Steam API and is built around the Native Steam API vis Steamworks.NET

## Heathen vs Steamworks.NET

Heathen Engineering's Steamworks are built on top of [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET). The [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) project is designed to be a direct 1 to 1 wrapper around Valve's Steam API wrapping the native C and C++ interfaces up in a C# plugin.

{% hint style="success" %}
[Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) is authored by [**Riley Labrecque**](https://github.com/sponsors/rlabrecque) and the only reason our Steam integrations exist.\
\
Pop over to his [sponsor page](https://github.com/sponsors/rlabrecque) and buy the man a beer at the very least.
{% endhint %}

[Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) gives the best access to Valve's APIs and does so true to the original, so that the original documentation and decades of community guidance are still applicable. The draw back to [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) is that it is true to the original API using programming styles and approaches foreign to most game developers and very clunky at best to use in Unity or Godot scripting.

Heathen has wrapped every relevant interface in Steamworks.NET with our own static [APIs ](api/)delivering a simpler more robust tool set with every drop of power of the source Steam API and with that raw Steam API still available to you.

Heathen's Steamworks does not replace [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) - it builds on top of it and provides you with a set of battle tested and developer approved tools and systems written with Unity in mind.&#x20;

## Heathen vs Facepunch

Facepunch is another C# wrapper just like Steamworks.NET. however unlike Steamworks.NET it does not attempt to remain true to the original API as a result the existing community and documentation around Steamworks is less applicable. &#x20;

Facepunch's stated goal is make a C# focused wrapper that is to exploit / leverage the benefits of C#. This makes most of the code you would need to write shorter / more C# programmer friendly. It however also makes it alien to Valve's documents and its wider community and while Unity uses C# as its main scripting language it does so in a "Unity" way for example C# would use event delegates, in Unity we use UnityEvents.

Heathen does similar in that we are here to make the Steam API more friendly to a specific audience, only we are Unity centric not just C# centric. We have wrapped the complexities of Steamworks.NET making it quick and easy to integrate for C# programmers, Unity specific programmers, Unity designers and hobbyist that prefer to use tools like Bolt or work through inspectors to get the job done. We chose to build on top of Steamworks.NET so that for the dev that wants/needs to they can still leverage the decades of community guidance on the source API only needing to convert C/C++ to C#.

Because we are built on top of Steamworks.NET which is its self a true to form wrapper around the native Steam APIs many tools, assets, etc. built for Steamworks.NET or Valve's original Steam API simply work, that is not the case for Facepunch which often requires its own flavour of a tool to work.

## Feature Comparison

Steamworks is available in two packages as described below.

{% hint style="info" %}
The full raw Steam API (in C#) is fully available in all versions via our Steamworks.NET integration.\
\
The "Features" shown here are Heathen extensions which make working with the API easier, safer, more robust and more functional but are not \*required\* in order to integration with Steam.&#x20;
{% endhint %}

| Features                                             | Foundation | Complete |
| ---------------------------------------------------- | ---------- | -------- |
| <p>Full API Supported by</p><p>Steamworks.NET</p>    | ✔          | ✔        |
| Initialization for client and server                 | ✔          | ✔        |
| Overlay                                              | ✔          | ✔        |
| Stats                                                | ✔          | ✔        |
| Achievements                                         | ✔          | ✔        |
| Friends                                              | ✔          | ✔        |
| User                                                 | ✔          | ✔        |
| **Networking** FishNetworking Compatibility          | ✔          | ✔        |
| **Networking** Mirror Compatibility                  | ✔          | ✔        |
| **Networking** NetCode for GameObjects Compatibility | ✔          | ✔        |
| App                                                  |            | ✔        |
| Authentication                                       |            | ✔        |
| Clan                                                 |            | ✔        |
| Data Model                                           |            | ✔        |
| DLC                                                  |            | ✔        |
| Game Server Browser                                  |            | ✔        |
| Input                                                |            | ✔        |
| Inventory                                            |            | ✔        |
| Leaderboard                                          |            | ✔        |
| Matchmaking (Lobby and Server)                       |            | ✔        |
| Parties                                              |            | ✔        |
| Remote Play                                          |            | ✔        |
| Remote Storage                                       |            | ✔        |
| Screenshots                                          |            | ✔        |
| User Generated Content (Workshop)                    |            | ✔        |
| Voice                                                |            | ✔        |
| Debugging Tools                                      |            | ✔        |
