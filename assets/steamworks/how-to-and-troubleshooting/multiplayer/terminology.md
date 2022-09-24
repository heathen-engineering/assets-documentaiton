---
description: Say what now?
---

# Terminology

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This is just a list of terms I will use in this article, they are not necessarily the right terms or standard terms, etc. again this is just me sharing info and this section is just meant to help you translate my dribble.

## Client

Client is a term that can mean many things. In general a "client" is a consumer of some service, a game for example as in the executable you run to play the game ... that is a "Game Client" even if there is no network its still a client. Within a single program such as your game you may have components that are acting as a "client" to other components that are acting as a "server" this is actually rather common.

In general networking when we say "Client" we mean that which is connected to a "Server". This gets more complex in P2P where one of the "Clients" is also the "Server" some networking APIs refer to this as "Host" as opposed to "Server" to try and differentiate the concepts.

## Game Loop

The flow the player takes through the game from start to finish and back to start again. You can think of this as the workflow of playing your game to use a more business style term.

## HLAPI

Aka a High-Level Application Program Interface … see what we say HLAPI now. When we use this, we are usually referring to a networking tool like Mirror, MLAPI, FishNetworking, Mirage, etc. they are APIs but not all of it. What they do is handle the relationship between your game objects and the network … they tend to refer to the network as LLAPI

## LLAPI

As noted in HLAPI this stands for Low Level Application Program Interface. When you’re talking about tools like Mirror, MLAPI, etc. they have a concept of a “transport” that is the part of the system that deals with sending and receiving information and handling connections. The interface that transports is built on … that is a LLAPI. In the case of Steam based networking solutions that would be SteamNetworking and SteamNetworkingSockets as the LLAPI that is used to create the various Steam Transports.

## Lobby

This term gets abused so very often by the developers of networking APIs.

{% hint style="danger" %}
A lobby is not a networking feature
{% endhint %}

A lobby is best thought of as a chat room. It exists before there is a network session set up at all, in fact its where your player's will meet to agree what kind of session should be set up. In most cases when the network session comes up and the player's join it, they would leave any matchmaking lobby they are in.

Lobbies can be used for loads of features that have nothing at all to do with networking or even multiplayer. They are fundamentally just a chat room associated with a Steam App that players who are running the same app can join, attach metadata to, search for, etc. This makes lobbies useful for matchmaking, player groups/parties they are used in Steam's remote play feature and through the parties system can be used to invite players to come play the game with you or watch you play the game over Steam Streaming.

Mirror, Photon and others have a concept of a "Room" ... this is not a lobby and not related to lobby.

A Room is not a lobby, its a strange concept used by some networking systems as a sort of pore mans matchmaking service. It really doesn't make any sense to me as to why you would use such a thing. It seems it would be easier to simply manage your network environment your self but to each there own just understand it is not a lobby and in no way related.

## NM

Network Manager, most HLAPIs have a concept of a network manager. This is your games main point of interaction with the network at least so far as starting and stopping a connection. The NM would be what references the transport or transports you wish to support and shuttles data between the rest of the HLAPI such as Network Behaviours to and from the LLAPI via those transports e.g., Send/Receive

## Room

We don't use this and don't recommend any one does. Room is a concept seen in Mirror, Photon and a few other networking solutions. Personally I see no reason to use such a thing especially if you have a proper backend service provider like Steam or PlayFab.

A room is a full network connection so really if you can connect to a room why not just go ahead and be connected to your session sense you already are.&#x20;

This concept is mostly used by people who let the network manager manage which scene is active, another thing we do not do not recommend. If you do let your network manager manage your scenes then read up on how "room" works with your API if at all.

If your managing your own scene structure (strongly recommended) then room offers no benefit and can be ignored.

## Server

Another often abused term.

In its simplest form a "server" is anything that serves other things. For example GitBook is a web server, serving your browser with HTML content.

A computer running a server OS used to server other computers with services is also a server

A Unity session that is being connected to by other Unity sessions is a game server

Unity builds can be both servers and clients and most NM's have a concept of "Host" which is exactly that, it is where your NM is acting as both a client and a server. That is it is asking for content (From its self) and serving that content (to its self and others).

A lobby however is not a server, browsing for lobbies is not a way to make a server list. Server discovery is a concept which Steam handles please see the [Steam Game Server](game-server-browser.md) and [Game Server Browser](../../components/game-server-browser-manager.md) for more information.

## Transport

Again, a common term with HLAPIs like Mirror, MLAPI, etc. This is referring to a simple object that acts as an adapter between you HLAPI and your LLAPI e.g., Fizzy Steam Transport lets the Mirror HLAPI talk to the SteamNetworking LLAPI
