---
layout:
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

# Learning

## Feature Guides

Look left 👀

Now scroll that navigation panel up till you see Steam

<figure><img src="../../.gitbook/assets/image (461).png" alt=""><figcaption></figcaption></figure>

Behold a series of guides on every aspect of Steam not restricted to Steamworks but including every feature of it and much more. Select a topic that suits you ... and read.

<figure><img src="../../.gitbook/assets/image (463).png" alt=""><figcaption></figcaption></figure>

The structure will vary by topic a bit but in general you will find a "Quick Start" along with Examples including common use cases. Note this applies to all engines and is even useful if your not using Heathen tools at all.

Each of these articles is meant to be a concise yet robust guide to each given topic.

## Object, Data, API Extension

With Unity, you have at least 3 ways to do anything. These 3 options all fundamentally do the same thing, they all compile down to the same result when built. They exist to support 3 major types of Unity developers.

1 is not better than the other, they all result in the same output and they all ultimately call the same underlying APIs. Note that each layer is built upon the layer below it, as a result, you can easily switch form one to the other mixing and matching as suits you at any given point for any given topic.

### API Extension

This is a full C# & Unity-centric wrap around the Steamworks SDK. It covers every feature of the Steamworks SDK with static classes, it handles every Steam Callback and CallResult in a Unity-centric manner (UnityEvent, Action, etc.) and it returns Unity-centric data types where applicable e.g. Get Avatar returns a Texture2D instead of the native byte\[]

This layer will be familiar for developers used to working with the raw Steamworks SDK or with working with Steamworks.NET or Facepunch Steamworks.

It is of value even to vetted engineers because it handles all of the boiler plates and includes a number of quality-of-life improvements speeding up your workflow and decreasing your maintenance time.

### Data&#x20;

Steamworks can be described as "artefacts" such as Stats, Achievements, Lobbies, Apps, DLC, Users and more. The Data Layer creates a Data struct for each of these concepts which encapsulates the features, functions and data of those concepts.

For example, the UseData struct is implicitly convertible and equatable with ulong, CSteamDI and can be created from uint or string (Hex ID). It defines static functions to "Get" user data from various sources, to list friends, to fetch avatar images and more.

In effect, the DataLayer is a highly performant and highly convenient expression of Steamworks functionality by artefact type.

Note that "Data" structs are always implicitly convertible with the native Steamworks type such as CSteamID and the underlying primitive type such as ulong this means they can be used interchangeably with those types.

### Objects, Components & Prefabs

Unity classically has been a very object-oriented engine. ScriptableObject, GameObjects, UnityObejct. These allow you to drag and drop and create relationships between "objects" in the editor and largely code free. For all Steamworks "artefacts" such as Stats, Achievements, Leaderboards, Items, Inputs, etc. we have created "Objects" as ScriptableObejcts that reside under your SteamSettings object. This means you can easily reference and drag and drop in the editor to create relationships between objects and to call each of these objects exposes all the functionality of those respective artefacts for example you can create an AchievementObejct myAch and call myAch.Unlock() to unlock it.

For non-artifacts e.g. system concepts we have created "Managers" and other components for example the Lobby Manager which is a component script that can be added to any GameObject and will expose the features and functions of a Steam Lobby so you can easily and largely code free connect your Unity UI to a Steam Lobby

Prefabs are available that demonstrate the use of all the major components as well as a detailed example scene that uses Objects, Components & Prefabs to "largely" code-free implement all major Steamworks features.

## Code Snip-its

{% hint style="success" %}
New Work In Progress Feature
{% endhint %}

These are component scripts located in the Example Scene folder. Each covers a single topic and is meant to be opened and read like a book. They are functional C# code demonstrating features and use cases for the topics they cover such as LeaderboardData, UserData, etc.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The components themselves are wrapped such that they will not compile in a build and are marked as deprecated to discourage blind copy and paste. You can however take snips of the code (copy small sections) to jump-start whatever it is you are doing rewriting as needed for your own logic.

Each Snipit contains "Example" functions demonstrating common and key features of the topic. You can selectively copy and paste or simply read and learn from these to help kick start your own C# scripts.

## Example Scenes & Prefabs

### Install&#x20;

As of v3.4 the asset will install as a Unity Package ... this means it has an entry in your Unity Package Manager and extras such as sample scenes and prefabs can be imported from there and do not automatically import.

***

Before you can use the example scene you need to connect some objects to the settings in your project. You can locate the SteamMain settings object in your Settings folder. This will have been created when the asset was installed, if it is missing you can cause it to be created by opening your Project Settings.

In each Tab section below we will outline what objects if any need to be connected. This can not be done at the time we created the sample scene because the Settings were created in your project when you installed it.

![](<../../.gitbook/assets/image (472).png>)\


***

To find the package, open Unity Package Manager, be sure you're looking in the "In Project" collection and be sure you're looking under the `Packages - Heathen Group` heading, not the `Pacakages - Asset Store` heading. There you will find the Samples tab with options to import the Example Scene and Prefabs.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

***

You will need to connect the achievements generated for app 480 to the related objects in the scene. Expand the `[Achievements]` GameObject and the `Center` GameObject within. There you will find a GameObject for each achievement composed of standard Unity UI objects such as Toogle.

<figure><img src="../../.gitbook/assets/image (475).png" alt=""><figcaption></figcaption></figure>

For each achievement, there are 4 places we need to set the reference. 1st let us set the Toggle so that when the button is clicked it will set the achievement as achieved or not. Note this doesn't call "store" so you won't see the popups but it is setting the value and when the App is shut down (When Unity and Visual Studio are closed) the last value set will be committed.&#x20;

<figure><img src="../../.gitbook/assets/image (473).png" alt=""><figcaption></figcaption></figure>

Connect the `Toggle` of each object to the corresponding Achievement Object

Within each Achievement object (Winner Button, Champion Button, etc.) you will find 3 UI components for the Icon, Name and Description, on each is a simple Component Script that uses an Achievement object ... set each

<figure><img src="../../.gitbook/assets/image (474).png" alt=""><figcaption></figcaption></figure>



***

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

***

To get Input connected we need to select the `[Input]` game object that can connect it to the Input-Action, Input-Set and Input-Layers in the generated Settings.

<figure><img src="../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

The names should make it obvious where each goes, click the field and select the desired object.

***

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
