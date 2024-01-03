---
description: Steamworks Multiplayer tools, systems & features.
---

# 🎮 Multiplayer

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Let’s start by saying this here:

Creating a game is hard work, creating a multiplayer game is extra hard work, and creating a massively multiplayer game is … well you get the idea. If this is your first game or even 5th game, I would personally recommend spending some more time creating smaller stand-alone projects you can get done from start to finish without complexities like multiplayer. With that out of the way let’s get started.

{% hint style="success" %}
This article covers Steam Multiplayer concepts for more general information on Multiplayer [game design](../../guides/design/) please see our [guide on that topic](../../guides/design/multiplayer/).&#x20;
{% endhint %}

## Unity&#x20;

The Networking tool you choose to use does not impact any of the concepts you will learn here.&#x20;

You can use any networking tool you like (NetCode for GameObjects, FIshNetworking, Mirror, etc.), if you want to use the SteamNetworkingSockets interface you should choose a networking tool that has an integration with it.

\
Fish Networking, Mirror and NetCode for GameObjects all have Steam transports that they or their community author. Heathen \*\***does not\*\*** author any of these transports and cannot provide support for them. These transports can be used alongside Heathen's Steamworks Complete and Foundation.

### Network Scene (or scenes)

You will have a scene that is used during your gameplay and is the one where you want the network to spawn any network objects. This could be more than one scene or a single scene depending on your game and what HLAPI you using. The important concept here is you have some scene that is loaded into before the network session starts.

Many HLAPIs can define Network Objects as part of a scene and initialize them on start-up. This can be handy but it can also make debugging a nightmare. Consider at least keeping the scene itself free of any networking concepts then have the server or host as the case may be spawn in the required items as they configure the environment for play.

This may sound like extra work but it keeps the scene small and flexible so you can easily use 1 scene for many session types and makes debugging and troubleshooting vastly easier as the network only gets involved when you say so.

### Player Controller (PC)

Keep your PC simple, think of the PC a bit like you might think of Unity's Event System or Input System.&#x20;

It probably shouldn't be a visual element in your game, rather it's there to capture the inputs of the player it represents and sync that over the network and notify all other players as that input changes.

It makes sense to store player-specific values on it but the player is not a character. In most of our use cases, our PC is just an IO sync tool with some state info like what team the player is a part of. We have the PC spawn character controllers as required and these character controls define the visuals, sync animations, store character health, level, etc.

### Scene Management

Many HLAPI have a very crude scene management feature.&#x20;

You don't need this, in my experience it only serves to make things more complicated. In reality, the network doesn't care what scene is loaded or not or what is active or not. Unity does as that defines what GameObjects are loaded where and which environment settings are active.

We find it best to have the client handle the load and unload of scenes as makes sense for them. A lot of this comes from the realization that Unity handles multi-scene nicely and that a scene doesn't need to represent a physical area in your game so letting a network system which is driven by network visibility drive that makes no sense.

[See this article for more](../../guides/design/multi-scene-architecture.md)

See [UX Complete](../../assets/ux/components/scenes-manager.md) for tools that can help you leverage the power of Unity's scene system

### Session Lobby

[First, read up on what a Lobby is and is not](matchmaking-tools.md).

Importantly a lobby is not a networking tool or part of your networking system but it is a tool commonly used for matchmaking ... a process that happens before you get to the networking part.

A Session Lobby is simply the lobby you use for matchmaking and preparing the session. You can use this lobby to gather players together and help them agree on the terms and rules of the session they want to play such as game type, map, character selection, team organization, etc. Steam lobby also gives you the means to notify members when the session is ready to connect to via the Set Game Server feature noted below.

### Set Game Server

A feature of Steam's Lobby system. SetGameServer is a method available to you on the [Lobby](../../toolkit-for-steamworks-sdk/unity/data-layer/lobby-data.md) and through the [Matchmaking ](../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md)API. Only the owner of the lobby can call this method.

What it does is when this is called it will cause an event to be raised on all the members of the lobby to notify them that the server's connection information has been set and they can now join it.

This should be called by the owner of the lobby when the network environment is ready for users to connect to it. E.g. this is called in P2P after the Host has called StartHost and configured the network environment. In Client/Server, it's called after the owner has allocated a server and configured it.

When this is called the owner can specify a CSteamID representing the Steam peer or Steam Game Server.

Users that join the lobby after the event has occurred will not get the event raised however they can test if it has already been set via&#x20;

```csharp
if(lobby.HasServer)
{
    NetworkManager.address = lobby.GameServer.id.ToString();
    NetworkManager.StartClient();
}
```

## Unreal

With Unreal, networking is a more integrated aspect of the engine. Synchronization is an engine concept and is not impacted by the use or lack of use of Steam API.&#x20;

{% hint style="danger" %}
Do not use the Online Subsystem Steam plugin\
\
It is not compatible with Heathen's Steamworks Complete and is built on an out-of-date version of the Steamworks API lacking many important features.\
\
The limitations and drawbacks of Online Subsystem Steam are one of many reasons to choose Heathen's Steamworks Complete for Unreal over Unreal's built-in solution.
{% endhint %}

For more information on [Online Subsystem](../../toolkit-for-steamworks-sdk/unreal/online-subsystem.md) check out our article in the Steamworks Unreal section.

Your ability to set up multiplayer games is not bound to Steam API. Steam does provide a low-level transport called Steam Networking Sockets and Heathen does provide an Unreal NetDriver for it.

{% hint style="info" %}
Steam Networking Sockets Net Driver is currently in preview and only available to GitHub Sponsors\
\
If you have a need for the NetDriver and would like to work with the community on its implementation and testing let us know on Discord.
{% endhint %}

### How do you list sessions?

Steam API has matchmaking and social solutions that are not limited to the concept of game sessions and can easily account for the functionality of Online Subsystem's Sessions.

#### [Lobby](matchmaking-tools.md)

Steam Lobby is a common tool used for matchmaking, parties, teams, and merge groups. It's actually not a great tool for session browsing as it was designed with matchmaking in mind. In matchmaking the system tries to match the player with the best "match" based on defined factors such as the age of the match, region of the player and the specifics of the type of game session the player is looking for.

Heahten's Steam Lobby tools can help you use Steam Lobby to its fullest, creating player parties and groups, quick matches, chat rooms and more. Steam Lobby can be advertised on the player's Rich Presence enabling friends to join the lobby from outside the game. The lobby invite system can be used to invite players who are not currently in the game if desired and much more.

#### [Game Server](game-server-browser/)

With Heathen's Steamworks Complete, you can register your dedicated servers as Steam Game Servers. This will cause them to list on the Steam Game Server Browser. It will issue them a Steam ID and enable them to leverage the Steam API for authentication, stats, achievements and more.

[Rich Presence](rich-presence.md)

Steam Rich Presence is a powerful system that can enable you to display rich data through the user's friends list. Including but not limited to details about a game session. This can be as simple as how to connect by exposing a "Join Game" button or it can go deeper showing groups of users and providing details about the player's session such as mode, character selection, win or loss and more.
