---
description: >-
  Heathen’s Steamworks is a set of tools, systems and editor extensions designed
  to make integrating Steam easier, faster, and more robust. Helping you Do More
  rather your a beginner or a pro.
cover: ../.gitbook/assets/Banner@8x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Introduction

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Do More

{% embed url="https://www.youtube.com/watch?v=6ujmZI1qUYI" %}

{% hint style="info" %}
[Become a Sponsor](../become-a-sponsor/) and get all of our tools for 15$ it's the best way to **Do More**!\


Available for Unity 3D and Godot (mono)\*\
\* [Foundation](https://github.com/heathen-engineering/SteamworksFoundation) is available for Godot now with Complete in development and coming soon.
{% endhint %}

We take the strength of Steamworks.NET, and the parody it has with the native APIs, and expand on that with engine-centric tools, editor extensions and more!&#x20;

Heathen's Steamworks Complete is the best possible option for Unity & Godot (mono) developers looking to integrate with Steam API.&#x20;

## Key Features

### Full Coverage

Heathen's Steamworks Complete covers every aspect of Valve's Steamworks API, but we are so much more than "Just Another API Wrapper". In addition to covering every interface of Steam API we have also built common systems and tools to cover not just all the boilerplate but also all those common use cases with battle-hardened tools ready for production.

### Build Upload Tool

Build and upload your game to Steam right from the Unity editor with our [Steam Content Builder](../steam/uploading-to-steam.md) integration.

### Networking Integrations

Heathen's Steamworks Complete works with the networking tools you already know and use. On Unity, we work with Mirror, FishNetworking and NetCode for GameObject projects to ensure compatibility and with Unreal the Steam Networking Sockets plugin is again compatible with our plugin.

### API Extensions

Engine-centric, we expose the raw Steam API for you of course so any sample code you find floating around on the web should work with little or no modification. Beyond that, we extend the APIs with engine-specific features.

These extensions can be as simple as handling engine textures, events, etc. or more involved such as abstracting away the complexity of Steam's traditional C style handling of collections e.g. friends lists, DLC lists, leaderboard results, etc. and making them more appropriate to the respective engine.&#x20;

Our goal is to expose the Steamworks SDK features in such a way that they feel like a native extension of the engine you are working with.

### Steam Artifacts&#x20;

Every Steam artefact (lobby, achievement, DLC, user, etc.) is handled in a way native to the engine. For Unity this is C# structs (DOTS, programmers) and ScriptableObejcts (designers, editors). For Unreal Blueprint exposed nodes and events.

### Components

Major systems and concepts have additional tooling built around them to save you time with common tasks. From reading and displaying records from a leaderboard to managing a Steam Lobby for player parties, game sessions quick matches and a lot more.

Heathen's Steamworks is more than just another wrapper, our components provide highly configurable but easy-to-use production-ready solutions to common use cases.

## Battle Tested

{% embed url="https://store.steampowered.com/curator/42461073-Made-with-Heathen" %}

Trusted by [thousands of developers](https://discord.gg/6X3xrRc) we have been hard at work on this tool for more than a decade. [The Steam Curator link above](https://store.steampowered.com/curator/42461073-Made-with-Heathen) is just a few of the works our community have published covering many genres and demonstrating a wide range of examples from small passion projects to major commercial products.

## Built for You

Our tools are built in layers from powerful APIs and Frameworks up to code-free solutions. No matter your need, skill level or discipline our tools can help you Do More!

{% hint style="success" %}
Whether you're new to Steam, or game development in general or maybe a seasoned veteran well capable with the Steam APIs, Heathen’s Steamworks can greatly accelerate your project and help you produce a more robust product that better leverages the services offered by Valve.&#x20;
{% endhint %}

From top to bottom, each layer offers a level of simplicity and abstraction, you can mix and match as required to meet your project's and team's needs.

### Prefab & Tool Layer

Provides a range of ready-to-use prefabs and simple script components that allow many common requirements to be handled completely code free. All are built on our easy-to-use Components Layer.

### Components Layer

We provide flexible and powerful tools in the form of component scripts and scriptable objects that simplify the use of every major Steam feature in the editor with little or no code required. All are built on our easy-to-use Data Layer.

### Data Layer

Our "data layer" is a set of structs and tools that simplify working with Steam's concepts and artefacts such as UserData, LeaderboardData, AchievementData and more. These greatly reduce the code and effort required to accomplish any task. All are built on our robust API Layer.

### API Layer

Every endpoint and interface of Valve's Steam API has been expressed in a C# and Unity (or Godot) centric API. This means no need to mess with callbacks, manage operation queues cast and convert between various primitive and native types, etc.

The API Layer coupled with the Data Layer empowers programmers and engineers to work more efficiently and maintainable with Steam API and is built around the Native Steam API vis Steamworks.NET

## Feature Comparison

Heathen's Steamworks integration is available in two forms

* Foundation\
  This is a lite version available for free and is a great alternative to raw Steamworks.NET or Facepunch in that it will handle the core of Steamworks integration for you reliable and tried and true manner.
* Complete\
  This is our "full fat" tool covering every aspect of the Steamworks API, providing you with invaluable tools, systems, components and code-free solutions to help you Do More with Steam API.

<table data-full-width="true"><thead><tr><th width="261.5">Features</th><th width="221">Foundation (free)</th><th width="217">Complete</th><th width="171">Steamworks.NET</th><th>Facepunch</th></tr></thead><tbody><tr><td>License</td><td><a href="https://github.com/heathen-engineering/SteamworksFoundation">Free</a></td><td><a href="../become-a-sponsor/">Sponsor ($15)</a><br><a href="https://assetstore.unity.com/packages/tools/integration/steam-api-steamworks-complete-246652">Unity Asset Store (75$)</a><br>Unreal Marketplace (coming soon)</td><td><a href="https://github.com/rlabrecque/Steamworks.NET">Free</a></td><td><a href="https://wiki.facepunch.com/steamworks/">Free</a></td></tr><tr><td>Full API Supported</td><td>✔</td><td>✔</td><td>✔</td><td>Mostly</td></tr><tr><td>Documentation</td><td>Knowledge Base</td><td>Knowledge Base</td><td>Valve Docs</td><td>Wiki</td></tr><tr><td>Support</td><td>Dedicated + Community</td><td>Dedicated + Community</td><td>GitHub Issues</td><td>Not Found</td></tr><tr><td><h3>Editor Tools</h3></td><td></td><td></td><td></td><td></td></tr><tr><td>Achievement UI Tools</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Build Upload Tool</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Chat UI Tools</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Group / Clan UI Tools</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>User Profile Tools</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Leaderboard UI Tools</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Lobby UI Tools</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Debugging Tools</td><td></td><td>✔</td><td></td><td></td></tr><tr><td><h3>Data Layer</h3></td><td></td><td></td><td></td><td></td></tr><tr><td>Achievements</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>App</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Group / Clan</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>DLC</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Game</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Input</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Inventory</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Leaderboard</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Lobby</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Stats</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>User / Friend</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Workshop</td><td></td><td>✔</td><td></td><td></td></tr><tr><td><h3>API Extensions</h3></td><td></td><td></td><td></td><td></td></tr><tr><td>Application</td><td>✔</td><td>✔</td><td></td><td> </td></tr><tr><td>Authentication</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Big Picture</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Groups / Clans</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>User / Friends</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Steam Input</td><td></td><td>✔</td><td></td><td></td></tr><tr><td><strong>Inventory</strong></td><td></td><td>✔</td><td></td><td></td></tr><tr><td><strong>Leaderboard</strong></td><td></td><td>✔</td><td></td><td></td></tr><tr><td><strong>Matchmaking</strong></td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Overlay</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Parties</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Remote Play</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Remote Storage (cloud)</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Screenshots</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Stats &#x26; Achievements</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>UGC (Workshop)</td><td></td><td>✔</td><td></td><td></td></tr><tr><td>Utilities</td><td>✔</td><td>✔</td><td></td><td></td></tr><tr><td>Voice</td><td></td><td>✔</td><td></td><td></td></tr></tbody></table>

## Heathen vs Steamworks.NET

Heathen Engineering's Steamworks are built on top of [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET). The [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) project is designed to be a direct 1 to 1 wrapper around Valve's Steam API wrapping the native C and C++ interfaces up in a C# plugin.

{% hint style="success" %}
[Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) is authored by [**Riley Labrecque**](https://github.com/sponsors/rlabrecque) and is the only reason our Steam integrations exist.\
\
Pop over to his [sponsor page](https://github.com/sponsors/rlabrecque) and buy the man a beer at the very least.
{% endhint %}

[Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) gives the best access to Valve's APIs and does so true to the original so that the original documentation and decades of community guidance are still applicable. The drawback to [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) is that it is true to the original API using programming styles and approaches foreign to most game developers and very clunky at best to use in Unity or Godot scripting.

Heathen has wrapped every relevant interface in Steamworks.NET with our static [APIs ](unity/api/)delivering a simpler more robust tool set with every drop of power of the source Steam API and with that raw Steam API still available to you.

Heathen's Steamworks does not replace [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) - it builds on top of it and provides you with a set of battle-tested and developer-approved tools and systems written with Unity in mind.&#x20;

## Heathen vs Facepunch

Facepunch is another C# wrapper just like Steamworks.NET. however, unlike Steamworks.NET it does not attempt to remain true to the original API as a result the existing community and documentation around Steamworks are less applicable. &#x20;

Facepunch's stated goal is to make a C# focused wrapper that exploits/leverages the benefits of C#. This makes most of the code you would need to write shorter / more C# programmer-friendly. It however also makes it alien to Valve's documents and its wider community and while Unity uses C# as its main scripting language it does so in a "Unity" way for example C# would use event delegates, in Unity we use UnityEvents.

whoHeathen does similar in that we are here to make the Steam API more friendly to a specific audience, only we are Unity-centric not just C# centric. We have wrapped the complexities of Steamworks.NET making it quick and easy to integrate for C# programmers, Unity-specific programmers, Unity designers and hobbyists who prefer to use tools like Bolt or work through inspectors to get the job done. We chose to build on top of Steamworks.NET so that the dev that wants/needs to can still leverage the decades of community guidance on the source API only needing to convert C/C++ to C#.

Because we are built on top of Steamworks.NET which is itself a true-to-form wrapper around the native Steam APIs many tools, assets, etc. built for Steamworks.NET or Valve's original Steam API simply work, that is not the case for Facepunch which often requires its own flavour of a tool to work.
