---
description: Getting started with Heathen's Steamworks.
cover: ../../../../.gitbook/assets/Unity Banner.jpg
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

# Getting Started

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Initialization

Initializing the Steam API is the first step and you have a few choices on how you do this.

{% embed url="https://www.youtube.com/watch?v=fdBrndgYJZI" %}
Video created using Toolkit for Steamworks Legacy
{% endembed %}

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>Component</h3></td><td><ul><li>Zero Code</li></ul></td><td><a href="../../../../.gitbook/assets/Screenshot 2023-01-30 111452.png">Screenshot 2023-01-30 111452.png</a></td><td><a href="gameobject-initialization.md">gameobject-initialization.md</a></td></tr><tr><td><h3>Object</h3></td><td><ul><li>Doesn't require a GameObject</li><li>Single line of code</li></ul></td><td><a href="../../../../.gitbook/assets/Screenshot 2023-01-30 111537.png">Screenshot 2023-01-30 111537.png</a></td><td><a href="scriptableobject-initialization.md">scriptableobject-initialization.md</a></td></tr><tr><td><h3>API</h3></td><td><ul><li>Doesn't require a GameObject</li><li>No ScriptableObject</li><li>Pure C#</li></ul></td><td><a href="../../../../.gitbook/assets/Screenshot 2023-01-30 111633.png">Screenshot 2023-01-30 111633.png</a></td><td><a href="api-initialization.md">api-initialization.md</a></td></tr></tbody></table>

## Features

Be sure to see the [Steamworks Guide](../../../../company/steam/steamworks/) and its sub-articles for more detail, follows is a quick list of major features you will find.

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Achievements</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>API</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>Authentication</td><td><a href="../../../../company/steam/steamworks/multiplayer/authentication.md">authentication.md</a></td></tr><tr><td>Cloud Save</td><td><a href="../../../../steam/cloud-save.md">cloud-save.md</a></td></tr><tr><td>Debugging</td><td><a href="../../../../company/steam/steamworks/#steam-debugging">#steam-debugging</a></td></tr><tr><td>Downloadable Content</td><td></td></tr><tr><td>Friend List</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>Input</td><td><a href="../../../../steam/input.md">input.md</a></td></tr><tr><td>Inventory</td><td><a href="../../../../company/steam/steamworks/inventory/">inventory</a></td></tr><tr><td>Item Store</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>Leaderboards</td><td><a href="../../../../company/steam/steamworks/leaderboard-object/">leaderboard-object</a></td></tr><tr><td>Lobby</td><td><a href="../../../../company/steam/steamworks/multiplayer/matchmaking-tools.md">matchmaking-tools.md</a></td></tr><tr><td>Matchmaking</td><td><a href="../../../../company/steam/steamworks/multiplayer/matchmaking.md">matchmaking.md</a></td></tr><tr><td>Microtransactions</td><td><a href="../../../../steam/inventory/microtransactions.md">microtransactions.md</a></td></tr><tr><td>Multi-Platform Project</td><td><a href="../../../../company/steam/steamworks/multi-platform-project.md">multi-platform-project.md</a></td></tr><tr><td>Multiplayer</td><td><a href="../../../../company/steam/steamworks/multiplayer/">multiplayer</a></td></tr><tr><td>Rich Presence</td><td><a href="../../../../company/steam/steamworks/multiplayer/rich-presence.md">rich-presence.md</a></td></tr><tr><td>Room Systems</td><td><a href="../../../../company/steam/steamworks/multiplayer/room-systems.md">room-systems.md</a></td></tr><tr><td>Running a Build</td><td><a href="../../../../company/steam/steamworks/running-a-build.md">running-a-build.md</a></td></tr><tr><td>Steam Game Server</td><td><a href="../../../../company/steam/steamworks/multiplayer/game-server-browser/">game-server-browser</a></td></tr><tr><td>steam_appid.txt</td><td><a href="../../../../company/steam/steamworks/steam_appid.txt.md">steam_appid.txt.md</a></td></tr><tr><td>Steam ID</td><td><a href="../../../../steam/csteamid.md">csteamid.md</a></td></tr><tr><td>Stats</td><td><a href="../../../../company/steam/steamworks/stats-object.md">stats-object.md</a></td></tr><tr><td>User Information</td><td><a href="../../../../company/steam/steamworks/user-information/">user-information</a></td></tr><tr><td>Voice</td><td><a href="../../../../steam/voice.md">voice.md</a></td></tr><tr><td>Workshop</td><td><a href="../../../../company/steam/steamworks/workshop/">workshop</a></td></tr></tbody></table>

## Architecture

Heathen's Steamworks is built in layers, each layer offers another step of abstraction simplifying use of the API and doing more work for you. The lowest or most fundamental layer of Heathen's Steamworks is Steamworks.NET and is very much a raw Steam API wrapper, the highest or most "out of the box" would be our Prefabs which can handle many common uses cases with zero code on your part.

Follows is a quick break down of each layer and what it was meant for. Note you can mix and match without any issue. Our design expects that you will leverage our "high" level objects like prefabs to handle boilerplate, common or low importance items for you code free while you may prefer to go 100% bespoke with other features to achieve that perfect fit for your game.

* [Prefabs](../../prefabs/)\
  We have a number of ready to use prefabs that can be dragged and dropped into your game and will just work with no additional code required.
* [Components](../../components/)\
  We have created a set of component scripts (aka MonoBehaviours) to cover virtually every aspect of Steam API letting you work in Editor and with visual code editors like Bolt with ease
* [Scriptable Objects](broken-reference)\
  We have created scriptable objects for all Steam artifacts (stats, achievements, inventory items, etc.) making it easy to reference them and work with them via ours or your own component scripts as well as in code editors like Bolt.
* [Data Layer](../../classes-and-structs/)\
  We have created highly efficient and easy to use C# structs for all Steam artifacts (stats, achievements, inventory items, etc.). These allow programmers to work against these objects more efficiently and with significantly less coding required on there part. All of our structs are implicitly convertible between the primitive type, Steam API native type and our more abstracted structs and classes.&#x20;
* [API Layer](../../api/)\
  We have wrapped all core Steam API interfaces with our own C# and Unity centric API wrapper. These API wrappers match 1 to 1 with the raw wrappers but do greatly simplify use such as replacing "Callback" and "CallResult" with UnityEvents and Action parameters. In addition we have created a number of "quality of life" features such as a queue system allowing you to queue multiple calls to the API for features that require 1 call be processed at a time such as Leaderboard queries.
* Steamworks.NET\
  The raw Steam API as defined by Valve simply wrapped in C#. This is not our work but the work of [Riley Labrecque](https://github.com/rlabrecque/Steamworks.NET). We are work with Riley wherever possible to support his efforts and help the wider Steam Developer community. Heathen's Steamworks is built on top of [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) and thus it and the full raw API are available to you and interoperable with our wider toolset.

## Networking

{% embed url="https://kb.heathenengineering.com/assets/steamworks/guides/multiplayer" %}

{% hint style="success" %}
Heathen's Toolkit for Steamworks and whatever HLAPI you choose to work with have no impact on each other at all. You will use Steamworks and your HLAPI of choice the same as you would without the other.
{% endhint %}

### Do I need Heathen's Toolkit for Steamworks?

You do **not** "require" the Toolkit to use Mirror, FishNetworking or NetCode for GameObject's or any other Steam transports. Those transports like our selves work with Steamworks.NET directly.

That said you will need to initialize, configure and manage the Steam API before SteamNetworking interfaces can be used. Our Toolkit for Steamworks both the Complete and Foundation packages make working with Steam API simple and stable. If you do not use Complete or Foundation you would need to use the raw Steam API to initialize and configure your Steam API integration yourself before your HLAPI could use the Steam transports.

### Examples?

Where can I find examples on using Heathen's Toolkit for Steamworks and (the HLAPI I chose)?

You can't because there is no need. Both Steamworks Complete and your HLAPI of choice work the same whether or not the other exists. Thus we do not have an example of using (your HLAPI of choice) alongside our Steamworks Complete.&#x20;

If you want to see an example of using your HLAPI of choice with your HLAPI's Steam transport then you should contact them. We have links to [Fish Networking, Mirror and NetCode for GameObjects in our articles](../../installation/networking-integrations.md) but any HLAPI that works with Steamworks.NET properly will work.

If you looking for examples of how to initialize, configure and use Steam API (in general) you will find various samples in the provided [sample scenes](../../../../toolkit-for-physics/physkit/sample-scenes/) and examples throughout our knowledge base.

If you are trying to wrap your head around creating a [multiplayer game on the Steam platform](broken-reference), we have an article for that as well. That article is not specific to any given HLAPI because the HLAPI you choose has no impact on the concepts involved.
