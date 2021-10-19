---
description: >-
  Heathen Engineering’s Steamworks V2 is a set of tools, systems and editor
  extensions designed to make integrating Steam Client API significantly easier,
  faster, and more robust.
---

# Steamworks

{% embed url="https://discord.gg/6X3xrRc" %}

{% embed url="https://assetstore.unity.com/packages/tools/integration/steamworks-v2-complete-190316" %}

{% embed url="https://www.youtube.com/playlist?list=PL2R4tvBs-r1ncN8Y7SoF5IX-WY6K2m9AT" %}

## Introduction

![](../../.gitbook/assets/SocialImage\_NoMarking.jpg)

Heathen Engineering’s approach with its Steamworks assets has been to take the strength of Steamworks.NET, and the parody it has with Valve’s original APIs, and extend that with Unity centric tools, editor extensions and more to make Steamworks.NET + Heathen the best possible option for Unity developers looking to integrate with Steam. You retain the strength of leveraging raw Steam API when and where you may wish, while having the benefit of not just C# focused but Unity focused tools and extensions as well as systems battle tested across many games from many Unity developers.

Whether you're new to Steam, Unity, or game development in general or a seasoned veteran well capable with the Steam APIs, Heathen’s V2 can greatly accelerate your project and help you produce a more robust product that better leverages the services offered by Valve. Heathen’s asset does not prevent you from using raw API calls in conjunction with its own extensions and tools. Many features of Steam API can be handled within V2 with little or no coding at all. In the same respect everything is built with respect to the programmer and the need to extend and expand. Modular, extensible, and supported by a large community of fellow developers. Heathen’s Steamworks V2 is the best solution for Unity developers looking to ship on the Steam platform.

{% embed url="https://heathen-engineering.mn.co/topics/2141330" %}

Heathen Engineering's Developer Network is home to community generated documents, walk throughs, tutorials and more.

## Heathen vs Steamworks.NET

Heathen Engineering's Steamworks Complete (and Foundation) are built on top of Steamworks.NET. The Steamworks.NET project is designed to be a direct 1 to 1 wrapper around Valve's Steam API wrapping the native C and C++ interfaces up in a C# plugin.

Steamworks.NET gives the best access to Valve's APIs and does so true to the original, so that the original documentation and decades of community guidance are still applicable. The draw back to Steamworks.NET is that it is true to the original API using programming styles and approaches foreign to most Unity developers and very clunky at best to use in Unity scripting.

Heathen Engineering's Steamworks Complete does not replace Steamworks.NET - it builds on top of it and provides you with a set of battle tested and developer approved tools and systems written with Unity in mind. You can still access the raw API without issue when and where you need and leverage Heathen's systems to greatly accelerate your project where you see fit.

## Heathen vs Facepunch

Facepunch is another C# wrapper just like Steamworks.NET. however unlike Steamworks.NET it does not attempt to remain true to the original API as a result the existing community and documentation around Steamworks is less applicable. &#x20;

Facepunch's stated goal is make a C# focused wrapper that is to exploit / leverage the benefits of C#. This makes most of the code you would need to write shorter / more C# programmer friendly. It however also makes it alien to Valve's documents and its wider community and while Unity uses C# as its main scripting language it does so in a "Unity" way for example C# would use event delegates, in Unity we use UnityEvents.

Heathen Engineering does similar in that we are here to make the Steam API more friendly to a specific audience, only we are Unity centric not simply C# centric. We have wrapped the complexities of Steamworks.NET up in handy tools making it quick and easy to integration for C# programmers, Unity specific programmers and Unity designers that prefer to use tools like Bolt or work through inspectors to get the job done. We chose to build on top of Steamworks.NET so that for the dev that wants/needs to they can still leverage the decades of community guidance on the source API only needing to convert C/C++ to C#.

Because we are built on top of Steamworks.NET which is its self a true to form wrapper around the native Steam APIs many tools, assets, etc. built for Steamworks.NET or Valve's orignal Steam API simply work, that is not the case for Facepunch which offten requires its own flavor of a tool to work.

## Feature Comparison

Steamworks is available in two packages as described below.

| Features                                         | [Foundation](https://assetstore.unity.com/packages/tools/integration/steamworks-v2-foundation-186949) | [Complete](https://assetstore.unity.com/packages/tools/integration/steamworks-v2-complete-190316) |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Steamworks.NET                                   | ✔                                                                                                     | ✔                                                                                                 |
| Steam Client Initialization                      | ✔                                                                                                     | ✔                                                                                                 |
| Steam Game Server Initialization                 | ✔                                                                                                     | ✔                                                                                                 |
| Steam Overlay                                    | ✔                                                                                                     | ✔                                                                                                 |
| Steam Stats                                      | ✔                                                                                                     | ✔                                                                                                 |
| Steam Achievements                               | ✔                                                                                                     | ✔                                                                                                 |
| Steam Friends Tools                              | ✔                                                                                                     | ✔                                                                                                 |
| Steam User Data Tools                            | ✔                                                                                                     | ✔                                                                                                 |
| **Networking** Fish Net (Beta) Compatability     | ✔                                                                                                     | ✔                                                                                                 |
| **Networking** Mirror Compatability              | ✔                                                                                                     | ✔                                                                                                 |
| **Networking** MLAPI Compatability               | ✔                                                                                                     | ✔                                                                                                 |
| Steam Authentication Tools                       |                                                                                                       | ✔                                                                                                 |
| <p>Steam Clans </p><p>aka Steam Groups</p>       |                                                                                                       | ✔                                                                                                 |
| Steam DLC                                        |                                                                                                       | ✔                                                                                                 |
| Steam Leaderboards                               |                                                                                                       | ✔                                                                                                 |
| <p>Remote Storage</p><p>aka Steam Cloud</p>      |                                                                                                       | ✔                                                                                                 |
| Data Model Tools                                 |                                                                                                       | ✔                                                                                                 |
| Steam Game Server Tools                          |                                                                                                       | ✔                                                                                                 |
| Steam Inventory                                  |                                                                                                       | ✔                                                                                                 |
| Steam Matchmaking (Lobby)                        |                                                                                                       | ✔                                                                                                 |
| Steam Matchmaking (Game Server)                  |                                                                                                       | ✔                                                                                                 |
| <p>User Generated Content</p><p>aka Workshop</p> |                                                                                                       | ✔                                                                                                 |
| Steam Voice                                      |                                                                                                       | ✔                                                                                                 |
| <p>Steam Inspector</p><p>Debugging tools</p>     |                                                                                                       | ✔                                                                                                 |

## Steamworks V1 vs V2

{% hint style="warning" %}
Steamworks V1is deprecated

It is strongly recommended that any new projects be created on Steamworks V2
{% endhint %}

Heathen Engineering has been developing its Steamwork's integration since Unity version 5. V1 as we refer to it is that original version that had been upgraded bit by bit over many years. V2 is a complete rewrite and restructuring implemented with the release of Unity 2019 LTS. The change was made to enable future development features that would not have been possible or at least not reasonable in the older V1 structure.

Heathen Engineering does not do annualized major updates. That is, we will not create a V3 until which time the V2 requires some major rework or change to warrant a "major" update.

## Debugging Tools

Steamworks Complete V2 ships with a new set of debugging tools making it easier than ever to get your game up and running with Steam features.

![Steam Inspector with the engine running on the App 480 Spacewars example](<../../.gitbook/assets/image (22).png>)

The Steamworks Inspector is available from the main menu at the top of the screen and during simulation (running) it can display the internal state of the API and all the linked artifacts.

![Steam Inspector showing the Lobbies tab](<../../.gitbook/assets/image (23).png>)

The Steamworks Inspector includes a lobby inspection tool that can show you the internal state of all connected lobbies including the lobbies metadata and each member's standard metadata such as "Is Ready"

![Steamworks Inspector showing the Inventory Editor tab](<../../.gitbook/assets/image (24).png>)

The Steamworks Inspector can do more than just show internal states, it can help you define your Steam Inventory item definitions using the Inventory Editor system. Drag and drop your item definitions on to the tool and it will provide you with an easy to use editor for the most common use cases. You can then generate the JSON output expected by Valve on the Steam Developers Portal.

