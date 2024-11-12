---
description: Lobby + Network Session before the game starts ... 🤔🤪💩
---

# 💬 Room Systems

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The concept of a "room" is one often asked about but isn't something for Steam to do for you.

Traditionally matchmaking and lobby systems are by design as light as possible and involve as little user interaction as possible. The most common idea is that the player should be able to press play and the game will take care of everything for them responding only once the game is ready to play... take a look at DOTA, Halo, LOL, or really any team-based multiplayer game for a typical example of a "Quick Match" lobby based matchmaking system.

Rooms differ completely, the idea is to get the player into some sort of network session right away even if the session is not ready to play the game properly. This may take the form of a sandbox or "room" the player can run around with a 3D avatar. You see these with games that are derived from mods such as Battle Royal as a side effect or hold over of the source games they originate from Arma for example.

### What is a room exactly?

This is when you have your players go ahead and join a networked session while waiting for other players to join, for game rules to be decided, etc. In short, it's like a lobby but goes ahead and creates the network connection and session before the game is ready to play.

{% hint style="info" %}
This is not necessary and annoys a great many players so be sure it suits your game design before committing to it.
{% endhint %}

## Advantages

Room systems can be a great fit for some types of games, particularly party games or games without teams like battle royales where it's important to keep the player constantly engaged.

## Disadvantages

Rooms systems have a lot more moving parts and thus more opportunities to break. In particular, they have more networking requirements than a traditional Quick Match system and generally use more resources in that a network session must be created and maintained before the game proper is ready to play, you are managing a networked game session ... while trying to gather players for a networked game session and need to initialize your proper game session while managing your room session.

## How To?

As noted this is not a Steam thing, this is wholly a matter of game design. A room is nothing special it's simply a term we use for a network session that isn't the main game's network session.&#x20;

Technically speaking you don't "end" the room session to start the game session, rather your simply transitioning from the "room" environment to the game environment when the game session is ready.

Steam API is used by some as a "poor man's discovery service" ... by that, we mean that your room may be wholly a networking topic and has nothing at all to do with Steam. Steam's lobby can be used to represent your "rooms" on the Steam system such that other players can search for and find them, be invited to them, etc.

This is typically a matter of having the "room" creator also create a Steam lobby and setting the lobby's GameServer data to the connection information for the room in question. Thus the technical implementation typically looks like this

### Room Creation

When a user wants to play the game they will search for a room ... for the typical indie dev, this means searching for a Steam Lobby. If a lobby is found they will join that lobby and connect to the related "room" e.g. network session. If there is no matching lobby the player will start a new "Room" so for example if you're using Mirror and a P2P network solution then you might do `NetworkManager.StartHost` once the "room" is created and ready you have this same player create a new Steam lobby and call [SetGameServer](../../../../toolkit-for-steamworks/unity/classes-and-structs/lobby-data.md#set-game-server) on it so that new joining members know the room is ready to join.

### Join Room

Assuming you find a lobby in your search your next step is joining the "room" it represents. When using a P2P style network structure you can typically assume that the "owner" of the lobby is the "Host" of the room. For Client Server or if you simply want to make fewer assumptions you can check if a lobby has a connection or not and what it is as such

```csharp
if(lobbyData.HasServer)
{
    var serverData = lobbyData.GameServer;
    //Server Data now contains the CSteamID of the host or if you're using 
    //TCP/UDP style connections the IP/Port to connect to
}
```

See [LobbyData.GameServer](../../../../toolkit-for-steamworks/unity/classes-and-structs/lobby-data.md#game-server) and [LobbyGameServer ](../../../../toolkit-for-steamworks/unity/classes-and-structs/lobby-game-server.md)for more information.

### Transitioning to Gameplay

At some point you will want to move your players from the "room" to the game session proper. This has nothing at all to do with Steam and keep in mind you are not closing 1 network session to create another you're just loading the players into the game session scene and closing the "room" scene in most cases.

All that said when the "room" is done being useful you probably want to do away with the lobby. To do so you generally want to have the owner of the lobby "[lock](../../../../toolkit-for-steamworks/unity/classes-and-structs/lobby-data.md#set-joinable)" the lobby so no one else can join it and then have every player in the lobby leave it as they start playing the "session" proper.

### Browsing / Finding Rooms

Before you can join a room and before you create one you probably want to search to see what "rooms" are available.&#x20;
