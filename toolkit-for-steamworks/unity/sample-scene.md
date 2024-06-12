---
cover: ../../.gitbook/assets/Unity Banner.jpg
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

# Sample Scene

{% hint style="success" %}
#### Like what you are seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

### Install&#x20;

As of v3.4 the asset will install as a Unity Package ... this means it has an entry in your Unity Package Manager and extras such as sample scenes and prefabs can be imported from there and do not automatically import.

To find the package, open Unity Package Manager, be sure you're looking in the "In Project" collection and be sure you're looking under the `Packages - Heathen Group` heading, not the `Pacakages - Asset Store` heading. There you will find the Samples tab with options to import the Example Scene and Prefabs.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Layout

<figure><img src="../../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure>

<table data-header-hidden data-full-width="false"><thead><tr><th width="517"></th><th></th></tr></thead><tbody><tr><td>Along the right-hand side of the screen, you will find a menu of available topics covered by the sample scene. You can select a topic by clicking it, this will present an interactive UI specific to that topic, each display is unique and will include any relevant instructions as well as a button <code>Knowledge Base</code> that will open the corresponding Knowledge Base entry for that topic.</td><td><img src="../../.gitbook/assets/image (397).png" alt="" data-size="original"></td></tr></tbody></table>



<figure><img src="../../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>

Some topics commonly requested go beyond what can be demonstrated effectively (or at all) in a Unity sample scene. Many reasons could prevent this such as dependency on tools not part of the Steamworks SDK and or dependency on the specific App configuration in the Steam Developer portal.

<figure><img src="../../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

Pages for these topics have been added to explain this, highlight relevant information and link you to the appropriate Knowledge Base article that can guide you further.

## Tabs

{% hint style="success" %}
The Toolkit is designed to enable and empower Hobbyists, Designers, Amateurs, Professionals, Engineers and everything in between. \
\
While the sample scene does demonstrate the features using prefabs, and component scripts and does so largely in a code-free manner. Our toolkit includes API extensions, DataLayer (reference-free pure code tools) and more enabling you to work with each feature of the Steamworks SDK in the manner that suits you best. \
\
This lets you go as "deep" or work as "lite" as suits you, your project and your team, and of course, you can mix and match going deep on project critical features and lite on topics that you just need to have work and get out of your way.
{% endhint %}

### Achievements

This is a code-free scene, meaning all the functional aspects such as unlocking achievements is done without writing any custom code. You can examine the GameObjects to see which components were used for each aspect of the system.

The `Knowledge Base` button will link you to the [Achievements ](../../steam/achievements.md)article in this Knowledge Base.

<figure><img src="../../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>

The Achievements tab assumes the project is configured for App ID 480 aka `Spacewars`. It presents Spacewars' 4 main achievements, displaying the achievement icons which are being loaded live from the Steam backend according to the unlock state the user currently has.

{% hint style="info" %}
Note the toggles default to the "off" state regardless of your actual achievement status so you may need to double-click the first time to cause the state to sync. This is a limitation of the sample scene, not the underlying Steamworks Toolkit
{% endhint %}

When toggled Unlocked you will notice a slight delay and the achievement icon will brighten.

<figure><img src="../../.gitbook/assets/image (400).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note the Steam popup may or may not appear, this is not a bug with the Toolkit it is a limitation of Unity and Steam Overlay.\
\
The Steam Overlay works by rendering the Steam client overtop (overlaying) your app's main window. As far as Steam is concerned Unity Editor is your app at this moment and it has many windows, not all of which update correctly and so the pop up which is part of the Overlay usually gets lost or renders in the corner of some panel often unnoticed at all.\
\
In a properly built and deployed game where the game has exactly 1 window, this is not an issue.
{% endhint %}

### Friends

This scene displays your friends list, it will display the groups and Nicknames you have set up for your friends and the status and where applicable game name that each is playing. It demonstrates the basic functionality of reading the user's friends and groupings and data about each user such as name, nickname, status, etc.

The `Knowledge Base` button will link you to the [User Information](../../company/steam/steamworks/user-information/) article.

<figure><img src="../../.gitbook/assets/image (401).png" alt=""><figcaption></figcaption></figure>

### Microtransactions

MTX (Microtransactions) cannot be demonstrated in a general sample scene in any meaningful way. Steam's Microtransactions requires you to define your "items" as part of the application's configuration on the Steamworks Portal and is only accessible to the app owner before the app is released. thus it's not possible to test or demonstrate on a generic test app.

We do however have significant tooling to help you with all aspects of Steam Inventory including but not limited to MTX. The `Knowledge Base` button will link you to the [Microtransactions ](../../steam/inventory/microtransactions.md)article which is a sub-article of the broader [Inventory ](../../company/steam/steamworks/inventory/)topic.

<figure><img src="../../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure>

### Multiplayer

Multiplayer is a huge overarching topic that has many different tools, systems and features depending on specifically what your looking to do. As such there is no simple general sample we can demonstrate these with meaningfully.

<figure><img src="../../.gitbook/assets/image (403).png" alt=""><figcaption></figcaption></figure>

We have a host of guides on this broad topic:

* [Multiplayer Design and Concepts](../../company/design/multiplayer/)\
  This article explores common terms, technologies the typical workflows we see games use but is not specific to Steam or even Unity. It's a solid starting point if you are new to multiplayer game development, even if you are a vet it's useful to glance over if only to normalize the terms we use to describe things.
* [Steam Multiplayer](../../company/steam/steamworks/multiplayer/)\
  This article is the top level of a family of articles that touches on every feature of Steamworks that enables, supports or is otherwise related to multiplayer.
  * [Getting Started](../../company/steam/steamworks/multiplayer/getting-started.md)\
    This is a quick summary document aimed at the most common use cases that gives you a short and to-the-point guide to kick-start you.
  * [Dev and Test](../../company/steam/steamworks/multiplayer/dev-and-test.md)\
    Methods and approaches to handling development and testing with a networked multiplayer game.
  * [Authentication](../../company/steam/steamworks/multiplayer/authentication.md)\
    Steam Authentication is not login, this covers what it is when you would use it. It has common uses cases and examples in both Unity and Unreal.
  * [Lobby](../../company/steam/steamworks/multiplayer/matchmaking-tools.md)\
    Perhaps the single most misunderstood feature of multiplayer and doubly so for Steam. Our guide on Steam Lobby goes in depth as to what Steam Lobby is, its features, common use cases and examples in both Unity and Unreal.
  * [Matchmaking](../../company/steam/steamworks/multiplayer/matchmaking.md)\
    A common topic of need that touches on Steamworks various tools and systems that help you with matchmaking needs.
  * [Rich Presence](../../company/steam/steamworks/multiplayer/rich-presence.md)\
    A feature of Steamworks that ties into matchmaking, game and lobby invites and general multiplayer session discovery.
  * [Room Systems](../../company/steam/steamworks/multiplayer/room-systems.md)\
    A commonly asked-about topic, this article covers what it is, what it is not, ways to go about it and alternatives you might consider.
  * [Steam Game Server](../../company/steam/steamworks/multiplayer/game-server-browser/)\
    This is another broad topic that helps you understand the Steam Game Server APIs and how to set up a Dedicated Server that works with Valve's Steamworks. The article has sub-articles on [Build](../../company/steam/steamworks/multiplayer/game-server-browser/builds.md), [Configuration](../../company/steam/steamworks/multiplayer/game-server-browser/configuration.md), [Server Browser](../../company/steam/steamworks/multiplayer/game-server-browser/server-browser.md) and [Server (OS) setup](../../company/steam/steamworks/multiplayer/game-server-browser/setup-linux.md).
  * [Terminology](../../company/steam/steamworks/multiplayer/terminology.md)\
    A simple article that defines some of the commonly used terms and tries to help you detangle the information that is already out there. Multiplayer and Networking in general is a minefield of word and alphabet soup where the same phrase or term might have many meanings depending on who says it and in what context.
* [Remote Play](../../steam/remote-play.md)\
  Steamworks Remote Play is a powerful system that enables a local multiplayer game to act like a network multiplayer game e.g. you can have a "local" player be "remote"

### Remote Storage (Cloud Save)

This sample demonstrates the Steam Remote Storage system with a simple form for creating, saving and loading data of Steam Remote Storage aka Steam Cloud. The `Knowledge Base` button will open the [Cloud Save](../../steam/cloud-save.md) article.

<figure><img src="../../.gitbook/assets/image (405).png" alt=""><figcaption></figcaption></figure>

Steam is capable of saving anything you can write to a file to its "cloud" and our tools simplify that making it feel much more like simply writing or reading to and from a file with built-in tools to automatically handle any serializable object.

### Input

This sample demonstrates the use of Steam Input with controllers, it does require that you have a controller active before you press play on the sample. It will display the correct button icons and the result of inputs read from the controller via Steam Input API. Its `Knowledge Base` button will open the [Input](../../steam/input.md) article.

<figure><img src="../../.gitbook/assets/image (406).png" alt=""><figcaption></figcaption></figure>

### Leaderboards

This sample demonstrates the use of leaderboards, displaying the local user's entry and the 10 nearest entries as well as providing a simple way to type in a value to upload to the board. The `Knowledge Base` the button will open the [Leaderboard ](../../company/steam/steamworks/leaderboard-object/)article.

<figure><img src="../../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure>

### Lobby

This sample is a simple demonstration of creating and joining a Steam lobby, displaying lobby members and handling lobby chat. The button can be used to create a lobby, or if you type in a lobby ID it can be used to join that lobby. When you are in a lobby it will present that lobbies Hex ID which can be used by other users to join that lobby. \
\
Steamworks has a host of features for inviting users, searching for lobbies, and advertising lobbies to others. Please see the `Knowledge Base` article [Lobby ](../../company/steam/steamworks/multiplayer/matchmaking-tools.md)for more info.

<figure><img src="../../.gitbook/assets/image (408).png" alt=""><figcaption></figcaption></figure>

### Workshop

This scene demonstrates browsing the Steam Workshop for the current title, as the sample uses App 480 Spacewars which is a demonstration app available to everyone it will have an absolute mess of entries most of which are incomplete or broken. The sample is here to demonstrate the concept the actual implementation is dependent on your game's needs and uses. Our toolkit does provide a host of tools to help you browse, create, upload and edit workshop items from within your game. The `Knowledge Base` button will take you to the [Workshop](../../company/steam/steamworks/workshop/) article with sub-articles on [Creating an Item](../../steam/workshop/creating-an-item.md), [In-Game Browser](../../company/steam/steamworks/workshop/in-game-browser.md) and handling [Subscribed Items](../../steam/workshop/subscribed-items.md).

<figure><img src="../../.gitbook/assets/image (409).png" alt=""><figcaption></figcaption></figure>

## Can't find the sample?

### Unity Asset Store

Look in the Examples folder you should see a single scene file there, double click to open it. ![](<../../.gitbook/assets/image (410).png>)

### GitHub Sponsor

As a GitHub Sponsor, you will have installed Heathen's Toolkit for Steamworks via the Unity Package Manager

![](<../../.gitbook/assets/image (2) (3).png>)

You can simply select Steamworks Complete in the Unity Package Manager expand the "Samples" drop-down and then import the Example Scenes ... this is also where you will find the uGUI Tools
