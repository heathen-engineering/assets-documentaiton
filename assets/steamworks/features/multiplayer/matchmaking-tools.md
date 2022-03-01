---
description: >-
  Understanding what a Steam lobby is and is not, getting started with Steam
  Lobby
---

# Steam Lobby

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/integration/steamworks-v2-complete-190316)asset.
{% endhint %}

Steam Matchmaking is driven primarily through the Steam Lobby feature. In a nutshell, the concept is that players will create a "lobby". You can think of this a bit like a chat room. This lobby has "metadata" associated with it which can be used to search for lobbies, filtering the results to just those the player cares about.‌

The metadata concept of Steam Lobby is where most of the functionality comes into play. The owner or "host" of a lobby can set the metadata on a lobby and anyone else can read that data, and the Steam Lobby search system can use that data to refine search results. In addition, each member within a lobby has a set of metadata associated with them. Lobby member metadata can only be set by the member it is related to and can only be read by other members of that lobby.‌

In summary lobby metadata is for stating the intent of the session or the status of the session and is accessible by everyone. Member metadata is for stating the intent of a member or the status of a member and is writable only by that member and readable only by fellow members of the same lobby.‌

You can read more about Steam's Matchmaking system on Valve's developer documentation.

{% embed url="https://partner.steamgames.com/doc/features/multiplayer#matchmaking" %}

## Key Concepts

### Lobby?

The first and most important thing to understand is that a lobby is not a network feature or concept. That is being in a lobby does not require a network connection, a network connection does not require a lobby. Lobby and Networking are two completely independent concepts.&#x20;

Please do not confuse a lobby with anything to do with a network or network connection.

### Lobby Types

The following explains; as clearly as Steam documentaiton allows, the available lobby types and when and how you might use them.

*   Private

    Classified as a "Normal" lobby by Steam.

    The only way to join a private lobby is to be invited to it via the Lobby.InvitePlayer feature. This can be useful in coop games when your player want to play with a specific friend but doens't want to be bothered by requests to join or public searches.

    This lobby will not appear in searches, it will not appear on the user's friends list or rich presence data.
*   Friends Only

    Classified as a "Normal" lobby by Steam.

    This lobby can only be joined by friends of the owner or by people directly invited to it. This lobby does appear on the user's friends list but does not appear in lobby lists or searches. This is useful when the player wants friends to be able to dorp in / out but doesn't want be bothered by random players.
*   Public

    Classified as a "Normal" lobby by Steam.

    This is the typical lobby you will see used in most games. Its the classic "Matchmaking" lobby that appears on the user's friends list and can be searched for and joined by any matching player.
*   Invisible

    This is the lobby type that Valve/Steam allows a user to be a member of 2 of

    This lobby is not visible in the friends list but can be searched for. That might be confusing at first read.

    A random user can search for this lobby as you would a public lobby but this lobby will not show up on the Steam Friends list hence "invisible"

### Metadata

Metadata refers to data stored on the lobby or on a lobby member. Put simply its a collection of key value pairs where the key and value are a simple string. So you can think of it much like a&#x20;

```csharp
Dictionary<string, string>
```

The metadata stored on the lobby can be seen by anyone able to see the lobby and can be used to  filter results when searching for a lobby using Steam's matchmaking system.

In contrast metadata stored on a lobby member can only be seen by members of the lobby and is used only to share for example user configuration.

When metadata is changed the Steam API will raise the lobby data changed event ... that event will indicate what object's data changed by not what data field changed so for example if the event indicates the lobby data changed you should check all the lobby metadata where as if it indicated a members data changed you should check that members metadata.

The event in question is exposed on the Lobby Manager as [evtDataUpdated ](../../components/lobby-manager.md#evtdataupdated)and in the Matchmaking API as [EventLobbyDataUpdate](../../api/matchmaking.md#eventlobbydataupdate).



As far as setting metadata you can use the indexers to set metadata for example if you have a `Lobby` in memory such as from the lobby manager.

```csharp
var lobby = lobbyManager.Lobby;
```

Then you can set a metadata field on it such as

```csharp
lobby["thisField"] = "thisValue";
```

Similarly if you have a `LobbyMember` in memory you can do the same thus

```csharp
var member = lobby.User;
member["thisField"] = "thisValue";
```

To learn more check out the [Lobby](../../objects/lobby.md#introduction) article describing the features of the lobby structure.

## Matchmaking

It is important to understand that a lobby is not a server browser, it is not designed to list all possible sessions. It is effectively a chat room and a matchmaking tool.&#x20;

### Can I list all? No

Steam API at most will return 50 lobbies and in most cases that is 49 more lobbies than you need. The lobby query system is designed such that your user describes they match they want and the Steam API will return the ideal match from the available lobbies.

> What if the exact match the player wants isn't available or what if they don't know exactly that they want?

In that case you have two options

### Quick Match

This is the most common approach by modern games. A quick match is where you search for a lobby that matches the desired game well enough and join it, if no ideal match can be found you create a new lobby with the arguments that match the ideal match and continue to look for near matches.

This means that other player's looking for the same match will find your new lobby and join you. Typically a modern game will also be looking for near matches in the background and after some tolerable time will take the nearest match even if its not ideal.

The objective of "Quick Match" in most games is to get the player playing a multiplayer match as soon as possible. Hence "quick" match. It does this by&#x20;

1. Searching for an ideal match
2. If not found creating an ideal lobby that others can join
3. If not enough join in a tolerated time joining the next best lobby it can find

### Lobby Browser

Another approach used is to display a list of "near match" lobbies to the user along with a "create lobby" button.

Older games didn't let you create a new lobby until you searched for one. Once the search failed it would display the nearest matches to your search arguments along with a create button. The idea here is a player should first fill up a waiting session or if none suit the player's needs create one of there own.

This model does much the same as Quick Match but lets the player decide what the "nearest match" lobby is. The down side to this is some players will be stubborn and always make there own  lobby increasing the average time to match for all players.

#### How to display lobbies

The [5 Lobbies](../../learning/sample-scenes/5-lobbies.md) sample scene demonstrates browsing for lobbies. If you wanted to do this model the ideal solution is to let the user define there search arguments and return a small number of the lobbies if any that match that say the top 10.&#x20;

You can then do searches that are slightly less strict ... what this means depends on your game. For example lets say your game is a classic shooter with modes like CTF, C\&H, KofH and has session sizes of 4v4, 8v8 and 16v16 and maybe also lets your player's pick a map.

Your player may search for CTF 4v4 on map X. You return the top 10 matches that suit that but show the player the top 10 CTF 8v8, top 10 C\&H 4v4, top 10 KofH 4v4, etc. You don't want to flood your player with to many options and you dont want to burry there preference the idea is to show them options in case there ideal match isn't available or in case they didn't think to look for something else.

### I need to list all servers

{% hint style="success" %}
A lobby is not a server

A lobby is a group of player's looking to play a game together.
{% endhint %}

Its keenly important that you understand that a lobby is not a server, it is not a networking concept at all. It is a chat room where player's meat and converse to decide what they would like to play together before they go do so.

You can think of it like jumping on Team Speak, or Discord, etc. and rounding up a few friends to go play a game together.

If you want to list a set of available server's then you 1st off need servers. You can look at creating a server build for your game and having it register as a [Steam Game Server](game-server-browser.md).

{% hint style="info" %}
Learn more [here](game-server-browser.md)
{% endhint %}

Once you have a server build you need to decide how your going to host it.

1.  Player Hosted

    This is where you ship your server build and let player's host it them selves
2.  Bespoke

    Services like [G-Portal](https://www.g-portal.com) can be used to host official, private, etc. ... you see this done a lot with survival games like Minecraft, Conan Exiles, etc.
3.  Traditional

    Using a service like [PlayFab](https://playfab.com), [GameSparks ](https://www.gamesparks.com)or [Multiplay](https://unity.com/products/multiplay)
4.  DIY

    Do it your self, if your a glutton for pain or just really like data operations you could of course host your servers your self.

Doing this will let you browse for and display all available (and publicly visible) stem game servers via a [Steam Game Server Browser](../../components/game-server-browser-manager.md).

## Use Cases

### Create a Lobby or Group.

For more information on lobby types see Valve's documentation [https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs](https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs)&#x20;

See the [API.Matchmaking](../../api/matchmaking.md#create-lobby) interface for details on creating a lobby. In addition the [Lobby Manager](../../components/lobby-manager.md) tools can help you create, join and manage a lobby for a specific function in your game.&#x20;

Lets say for example you use 2 types of lobbies in your game

*   Party

    This would be where you have your player gather a group of friends together to play together i.e. a group or party as seen in MMOs, MOBA or really any game with a coop feature
*   Session Lobby

    This would be where you have your player's configure a game play session and wait for competitors to join or similar. This is the most typical use of a lobby and what drives matchmaking in your game.

In the above use case you would attack a [Lobby Manager](../../components/lobby-manager.md) to your Party UI and another to your Session UI. You would configure each accordingly and each can manage its own chat and metadata features. This helps you split functionality across concepts unique to your game.

### Find and Join Lobbies

The easiest way to search for and join lobbies is through the [Lobby Manager](../../components/lobby-manager.md) tool. Alternatively you can use Heathen's API.Matchmaking directly to easily search for and join lobbies.&#x20;

Aside from browsing for a lobby you can handle invite and joining of lobby invites. Inviting a friends to lobby can be done in a number of ways including from outside of your game via the Steam Friends list.

Internally to you game you can use the [User Data](../../objects/user-data.md) object to invite a specific player. You would have access to this object from various tools and interfaces including [Friends](../../api/friends.md), [Clans ](../../api/clans.md)and there related chat systems. When you send an invite it is up to that user to accept it and there are multiple use cases for how they might accept the invite

#### While In game

In this case the accepting user is already in game and so the Game Lobby Join Invite event will be raised on the [Overlay Manger](../../components/overlay-manager.md#events) and its related [API.Overlay](../../api/overlay.md#game-lobby-join-requested) interface.

#### While out of game

In this case the accepting user is not yet in game and so the Steam client will launch the game and pass as an argument on the command line the lobby connection information. It is up to you to handle this argument, navigate to the appropriate place in your game e.g. the lobby UI and then join the lobby ID indicated on that argument.

A crude example follows

```csharp
// Return the ulong value of the lobby to join if any
public static ulong GetSteamLobbyInvite()
{
    var args = Environment.GetCommandLineArgs();
    ulong value = 0;
    for (int i = 0; i < args.Length; i++)
    {
        if (args[i] == CommonCommands.SteamLobbyConnect 
            && i + 1 < args.Length 
            && ulong.TryParse(args[i + 1], out value))
            return value;
    }

    return value;
}
```

Then you can perform the following

```csharp
var targetLobby = GetSteamLobbyInvite();
if(targetLobby > 0)
{
    //TODO: navigate to the Lobby UI in your game
    //Join the lobby
    API.Matchmaking.Client.JoinLobby(targetLobby);
}
```

### Using Lobby Chat

Steam's Lobby system includes a simple chat system able to handle text or data. The easiest way to interact with lobby chat is via the [Lobby Chat Director](../../components/lobby-chat-director.md) which needs to be added to the same object as your [Lobby Manager](../../components/lobby-manager.md).

You can also interact with lobby chat manually through the [API.Matchmaking](../../api/matchmaking.md) interface.

### Notify "Connect to network"

The typical purpose of a lobby is to gather player's and settle on the rules and conditions of the multiplayer session. In most cases you will at some point want to notify player's that they should connect to a particular server be that a Peer in a P2P game or a dedicated server on the net.

The lobby system provides tools for this via the `SetGameServer` method on the lobby

```csharp
public void Lobby.SetGameServer()

public void Lobby.SetGameServer(CSteamID gameServerId)

public void Lobby.SetGameServer(string address, ushort port)

public void Lobby.SetGameServer(string address,
                                ushort port,
                                CSteamID gameServerId)
```

{% hint style="warning" %}
The SetGameServer method can only be called by the "Owner" of the lobby
{% endhint %}

When called Valve will record the information on the Steam Lobby metadata as shown below

![](<../../../../.gitbook/assets/image (65).png>)

Each member of the lobby (other than the owner) will be notified by callback which raises the `EventLobbyGameCreated` event located on the [API.Matchmaking](../../api/matchmaking.md) interface and exposed through the [Lobby Manager](../../components/lobby-manager.md).&#x20;

{% hint style="warning" %}
All members of a lobby should upon joining the lobby register an event handler on the `Lobby.evtGameServerSet` event

```csharp
API.Matchmaking.Client.EventLobbyGameCreated.AddListener(HandleGameServerSet);
```
{% endhint %}
