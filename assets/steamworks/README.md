---
description: >-
  Heathen’s Steamworks is a set of tools, systems and editor extensions designed
  to make integrating Steam easier, faster, and more robust. Helping you Do More
  rather your a beginner or a pro.
cover: ../../.gitbook/assets/SteamMarketing Inventory hStretch.png
coverY: 17.4
---

# Steamworks

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="./">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/concepts/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="success" %}
Available for Unity 3D and Godot (mono)\*\
\
\* [Foundation](https://github.com/heathen-engineering/SteamworksFoundation) is available for Godot now with Complete in development and coming soon.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=6ujmZI1qUYI" %}

Heathen’s approach is to take the strength of Steamworks.NET, and the parody it has with Valve’s original APIs, and extend that with engine centric tools, editor extensions and more to make Steamworks.NET + Heathen the best possible option for Unity & Godot (mono) developers looking to integrate with Steam.&#x20;

With Heathen's Steamworks You retain the strength of directly accessing Steam API when and where you may wish, while having the benefit of not just C# focused but engine focused tools and extensions as well as systems battle tested across [many games](https://store.steampowered.com/curator/42461073-made-with-heathen) from many developers. We have wrapped [all relevant Steam interfaces in our API](api/) accounting for every callback and callresult in them, even the undocumented ones. Our knowledge base outlines every available interface, event, attribute, function and feature as well as every tool, system and object we have created on top of them.

Whether you're new to Steam, or game development in general or maybe a seasoned veteran well capable with the Steam APIs, Heathen’s Steamworks can greatly accelerate your project and help you produce a more robust product that better leverages the services offered by Valve.&#x20;

Heathen’s asset does not prevent you from using raw API calls in conjunction with its own extensions and tools. Many features of Steam API can be handled within Heathen's tools with little or no coding at all. In the same respect everything is built with respect to the programmer and the need to extend and expand without limitation.&#x20;

Modular, extensible, and supported by a large community of fellow developers. Heathen’s Steamworks is the best solution for Unity & Godot (mono) developers looking to ship on the Steam platform.

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
