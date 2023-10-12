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


Available for Unreal, Unity and Godot (mono)\*\
\* [Foundation](https://github.com/heathen-engineering/SteamworksFoundation) is available for Godot now with Complete in development and coming soon.
{% endhint %}

We take the strength of Steamworks.NET, and the parody it has with the native APIs, and expand on that with engine-centric tools, editor extensions and more!&#x20;

Heathen's Steamworks Complete is the best possible option for Unreal, Unity & Godot (mono) developers looking to integrate with Steam API.&#x20;

## Key Features

### Full Coverage

Heathen's Steamworks Complete covers every aspect of Valve's Steamworks API, but we are so much more than "Just Another API Wrapper". In addition to covering every interface of Steam API we have also built common systems and tools to cover not just all the boilerplate but also all those common use cases with battle-hardened tools ready for production.

### Build Upload Tool

In the editor Build Upload tools available for [Unity](unity/build-upload-tool.md) and [Unreal ](unreal/packaging-tool.md)(coming soon).

### Networking Integrations

#### Unreal

Works with Unreal Engine's Steam Sockets plugin

#### Unity

Works with Steam Networking Sockets Transports available for NetCode for GameObjects, Mirror and FishNetworking.

### API Extensions

Engine-centric, we expose the raw Steam API for you of course so any sample code you find floating around on the web should work with little or no modification. Beyond that, we extend the APIs with engine-specific features.

These extensions can be as simple as handling engine textures, events, etc. or more involved such as abstracting away the complexity of Steam's traditional C style handling of collections e.g. friends lists, DLC lists, leaderboard results, etc. and making them more appropriate to the respective engine.&#x20;

Our goal is to expose the Steamworks SDK features in such a way that they feel like a native extension of the engine you are working with.

### Engine Native

#### Unreal

Blueprint functions and bindable events, ready-made systems and widgets for common use cases. Engine native approach to Game Insnace, Save Game and more!

#### Unity

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

Provides a range of ready-to-use prefabs and simple script components that allow many common requirements to be handled completely code-free. All are built on our easy-to-use Components Layer.

### Components Layer

We provide flexible and powerful tools in the form of component scripts and scriptable objects that simplify the use of every major Steam feature in the editor with little or no code required. All are built on our easy-to-use Data Layer.

### Data Layer

Our "data layer" is a set of structures and tools that simplify working with Steam's concepts and artefacts such as UserData, LeaderboardData, AchievementData and more. These greatly reduce the code and effort required to accomplish any task. All are built on our robust API Layer.

### API Layer

Every endpoint and interface of Valve's Steam API has been expressed in a C# and Unity (or Godot) centric API. This means no need to mess with callbacks, manage operation queues cast and convert between various primitive and native types, etc.

The API Layer coupled with the Data Layer empowers programmers and engineers to work more efficiently and maintainable with Steam API and is built around the Native Steam API vis Steamworks.NET

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

## Heathen vs Online Subsystem Steam

Put bluntly [Online Subsystem Steam](https://docs.unrealengine.com/5.3/en-US/online-subsystem-steam-interface-in-unreal-engine/) is an incomplete solution. It does not cover the full Steam API and is limited to a handful of modules, what it does cover it only partially covers.

You can see a more l[ine by line breakdown of Heathen vs Online Subsystem Steam in our Unreal article](unreal/).

Heathen's Steamworks Complete is as its name suggests a complete integration of every aspect of Valve's Steamworks with the engine. It goes well beyond a simple API wrapper and provides you with ready-made and proven tools. The full Steam API is exposed to you in both C++ and Blueprint Functions, we also provide you with a set of common-use [UI Widgets](unreal/widgets/) and Unreal-centric tools like our [Steam Remote Storage Save Game](unreal/save-game.md) base class, [Steam Game Instance](unreal/game-instance.md) and more.

## Heathen vs Steam Core

Steam Core is a plugin available from the Unreal Marketplace and is "another Steam API wrapper". It provides more coverage than you get with Epic's own Online Subsystem Steam but doesn't cover the full Steam API. It also (appears) to make improper use of Steam API in a few key areas for example its approach to Steam Remote Storage (aka Steam Cloud) is to save the game to the disk using Unreal's Save Game and then read that file from the disk to save it to Steam Remote Storage ... this is exactly what Valve says you shouldn't do as you will end up with sync issues, it also doubles the disk space the save uses since Steam Remote Storage also writes the file to disk before syncing to Valve's backend.

The major difference between Heathen and frankly any other option is that Heathen has been doing this for over a decade, we have supported thousands of developers shipping hundreds of games on Steam. Our tools are well-designed and adhere to Valve's and the engine's best practices, our tools are more than just a Steam API wrapper, they let you leverage our extensive experience with the Steam API and Steam platform.
