---
description: Say what now?
---

# 🗣 Terminology

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This is just a list of terms I will use in this article, they are not necessarily the right terms or standard terms, etc. Again this is just me sharing info and this section is just meant to help you translate my dribble.

## Client

The client it's is a term that can mean many things. In general a "client" is a consumer of some service, a game for example as in the executable you run to play the game ... that is a "Game Client" even if there is no network it is still a client. Within a single program such as your game, you may have components that are acting as a "client" to other components that are acting as a "server" This is rather common.

In general, networking when we say "Client" we mean that which is connected to a "Server". This gets more complex in P2P where one of the "Clients" is also the "Server" Some networking APIs refer to this as "Host" as opposed to "Server" to try and differentiate the concepts.

## Game Loop

The flow the player takes through the game from start to finish and back to start again. You can think of this as the workflow of playing your game to use a more business-style term.

## HLAPI

A Unity Specific term: aka a High-Level Application Program Interface … see what we say HLAPI now. When we use this, we are usually referring to a networking tool like Mirror, MLAPI, FishNetworking, Mirage, etc. They are APIs but not all of them. What they do is handle the relationship between your game objects and the network … they tend to refer to the network as LLAPI

## LLAPI

A Unity Specific term: As noted in HLAPI this stands for Low Level Application Program Interface. When you’re talking about tools like Mirror, MLAPI, etc. they have a concept of a “transport” that is the part of the system that deals with sending and receiving information and handling connections. The interface that transports is built on … that is a LLAPI. In the case of Steam-based networking solutions that would be SteamNetworking and SteamNetworkingSockets as the LLAPI that is used to create the various Steam Transports.

## Lobby

This term gets abused very often by the developers of networking APIs.

{% hint style="danger" %}
A lobby is not a networking feature
{% endhint %}

A lobby is best thought of as a chat room. It exists before there is a network session set up at all it's where your players will meet to agree on what kind of session should be set up. In most cases when the network session comes up and the players join it, they would leave any matchmaking lobby they are in.

Lobbies can be used for loads of features that have nothing at all to do with networking or even multiplayer. They are fundamentally just chat rooms associated with a Steam App that players who are running the same app can join, attach metadata to, search for, etc. This makes lobbies useful for matchmaking, and player groups/parties are used in Steam's remote play feature and through the parties system can be used to invite players to come to play the game with you or watch you play the game over Steam Streaming.

Mirror, Photon and others have a concept of a "Room" ... this is not a lobby and not related to a lobby.

A Room is not a lobby, it's a strange concept used by some networking systems as a sort of pore man's matchmaking service. It doesn't make any sense to me as to why you would use such a thing. It seems it would be easier to simply manage your network environment yourself self but to each, their own just understand it is not a lobby and in no way related.

## NetDriver

A Unreal Specific term: this is similar to the Unity concept of a "[Transport](terminology.md#transport)" in that it is the low-level technology that handles sending and receiving data over a network. It generally also defines what a connection is and how it is addressed.

For example, Steam Socket-based NetDrivers can use either a Steam ID as an address or an IP:Port though generally, Steam ID is the way to go ... for example, an address might look like `steam.123456789123456789` where the number is the int64 value of the target system or user's Steam ID.

## NM or Network Manager

A Unity-specific term: Network Manager, Most HLAPIs have a concept of a network manager. This is your game's main point of interaction with the network at least so far as starting and stopping a connection. The NM would be what references the transport or transports you wish to support and shuttles data between the rest of the HLAPI such as Network Behaviours to and from the LLAPI via those transports e.g., Send/Receive

## P2P or Peer to Peer

This term gets abused and this time my Valve (Steam) directly. With regards to Steam documentation a "Peer" is anything that has a Steam ID, so Users but also Steam Game Servers. This means as far as Seam is concerned communication between a Steam Game Server (dedicated) and a Steam User (client) that is "P2P".&#x20;

For the entire rest of the world and even in contexts that are not networking ... a "Peer" is that which is the same as you. So Client to Client or Server to Server. Therefore in game networking when we say the game is "P2P" we (unless we are Valve" mean that there is no server, game clients connect to game clients e.g. Player to Player connection with no server at all.

## Room

We don't use this and don't recommend anyone does. Room is a concept seen in Mirror, Photon and a few other networking solutions. I see no reason to use such a thing especially if you have a proper backend service provider like Steam or PlayFab.

A room is a full network connection so really if you can connect to a room why not just go ahead and be connected to your session since you already are?&#x20;

This concept is mostly used by people who let the network manager manage which scene is active, another thing we do not recommend. If you do let your network manager manage your scenes then read up on how "room" works with your API if at all.

If you managing your scene structure (strongly recommended) then the room offers no benefit and can be ignored.

## Server

Another often abused term.

In its simplest form a "server" is anything that serves other things. For example, GitBook is a web server, serving your browser with HTML content.

A computer running a server OS used to serve other computers with services is also a server

A Unity session that is being connected to other Unity sessions is a game server

Unity builds can be both servers and clients and most NM's have a concept of "Host" which is exactly that, it is where your NM is acting as both a client and a server. That is it is asking for content (From itself and serving that content (to itself and others).

A lobby however is not a server, browsing for lobbies is not a way to make a server list. Server discovery is a concept that Steam handles please see the [Steam Game Server](game-server-browser/) and [Game Server Browser](../../../../toolkit-for-steamworks-sdk/unity/components/game-server-browser-manager.md) for more information.

### Listen Server

The technically correct term for a "host" or a Client that is also a Server such as used in Mesh and Peer to Peer based network structures.

### Dedicated Server

The technically correct term for a build that does nothing but server, that is there is no client here. This is sometimes also called a Headless Build.

### Steam Game Server

We have an article on this here. In short, a Steam Game Server is when you have your "Dedicated Server" e.g. your "Headless Build" register itself on Steam's backend such that it can use Steam Game Server APIs such as Steam Networking Sockets and such that Valve can issue it a Steam ID enabling it to be addressed as a Steam ID.

## Transport

A Unity-specific term: Again, a common term with HLAPIs like Mirror, MLAPI, etc. This refers to a simple object that acts as an adapter between your HLAPI and your LLAPI e.g., Fizzy Steam Transport lets the Mirror HLAPI talk to the SteamNetworking LLAPI
