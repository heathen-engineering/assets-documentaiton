# Terminology

## Client

Client is a term that can mean many things. In general a "client" is a consumer of some service, a game for example as in the executable you run to play the game ... that is a "Game Client" even if there is no network its still a client. Within a single program such as your game you may have components that are acting as a "client" to other components that are acting as a "server" this is actually rather common.

In general networking when we say "Client" we mean that which is connected to a "Server". This gets more complex in P2P where one of the "Clients" is also the "Server" also know as a "Host" some networking APIs refer to this as "Host" as opposed to "Server" to try and differentiate the concepts.

## Client / Server

This is a type of network topology that describes a "client" connecting to a "server" specifically when this term is used it means that a Game Client is connecting to a remote Game Server that is running on some machine somewhere else such as hosted in the cloud. This contrasts with "Peer to Peer".

## Game Loop

The flow the player takes through the game from start to finish and back to start again. You can think of this as the workflow of playing your game to use a more business style term. Some times when we say game loop we actually mean a sub-loop with in your game for example "combat loop" might refer to the flow of combat and in the context of a combat article or section might simply be called "the game loop".

## High Level Application Program Interface ( HLAPI )

Aka a High-Level Application Program Interface … see what we say HLAPI now. When we use this, we are usually referring to a networking tool like Mirror, MLAPI, FishNetworking, Mirage, etc. they are APIs but not all of it. What they do is handle the relationship between your game objects and the network … they tend to refer to the network as LLAPI

## Host

Most commonly this means a "Client" that is acting like a "Server" in a Peer to Peer network session.

## Low Level Application Program Interface ( LLAPI )

As noted in HLAPI this stands for Low Level Application Program Interface. When you’re talking about tools like Mirror, MLAPI, etc. they have a concept of a “transport” that is the part of the system that deals with sending and receiving information and handling connections. The interface that transports is built on … that is a LLAPI. In the case of Steam based networking solutions that would be SteamNetworking and SteamNetworkingSockets as the LLAPI that is used to create the various Steam Transports.

## Lobby

This term gets abused so very often by the developers of networking APIs making it one of the hardest things to understand when first starting out.

{% hint style="danger" %}
A lobby IS NOT a networking feature
{% endhint %}

A lobby is best thought of as a chat room or meeting place. It exists before there is a network session set up at all, in fact its where your player's will meet to agree what kind of network session should be set up. In most cases when the network session comes up and the player's join it, they would leave the lobby they had meet in.

Lobbies can be used for loads of features that have nothing at all to do with networking or even multiplayer. Exsactly what all you can do with the concept of lobby really depends on what tools, APIs and backend services your using in your game. For example Steam API has a concept of lobby that ties into matchmaking, friend groups and so much more.

PS: A Room IS NOT a lobby, its a strange concept used by some networking systems as a sort of pore mans matchmaking service. It really doesn't make any since if you stop to think about what its really doing. See the entry for "Room" in this article for more information.

## Network Manager ( NM )

Network Manager, most HLAPIs have a concept of a network manager. This is your games main point of interaction with the network at least so far as starting and stopping a connection. The NM would be what references the transport or transports you wish to support and shuttles data between the rest of the HLAPI such as Network Behaviours to and from the LLAPI via those transports e.g., Send/Receive

## Peer to Peer

This is a type of network topology that describes a "client" connecting to another "client" as opposed to a separate server such as one hosted in the cloud. This contrasts with Client / Server.

## Room

{% hint style="info" %}
This is a messy term with little value so we avoid using it.
{% endhint %}

This can mean a few things but when its your HLAPI or your network service provider talking about it ... this is a concept that needs to go die in a whole somewhere.&#x20;

### Network API Concept

What this really is, is a network connection to an assumed point aka the "room". Its used by a few tools as a sort of pore mans discovery system or as a pore mans matchmaking system.&#x20;

{% hint style="warning" %}
In my opinion ... which I am sure will irritate many networking API authors

Networking API's often have the miss notion that they are somehow the foundation of the system and they tend to try and ham fist in features a networking API has no business messing with. Common offending systems include but are not limited to

* Scene Management ( part of many Network Managers )
* Matchmaking ( Rooms )&#x20;
* Discovery ( Rooms )
{% endhint %}

### Game Design Concept

In game design when you hear developers talk about a "room" they are either talking about

A lobby; that is the point before the network session starts up where player's meet and decide the rules of the session they will play together.

or

The network session, that is the game "room" where players are playing together.&#x20;

## Server

( Also ) often abused:

In its simplest form a "server" is anything that serves other things. For example GitBook is a web server, serving your browser with HTML content enabling you to read this article.

A computer running a server operating system used to server other computers with various services is also called a server

A Unity session that is being connected to by other Unity sessions is a game server

Unity builds can be both servers and clients and most NM's have a concept of "Host" which is exactly that, it is where your NM is acting as both a client and a server. That is it is asking for content (From its self) and serving that content (to its self and others).

A Lobby however is not a server, browsing for lobbies is not a way to make a server list. Server discovery is a separate concept.

## Transport

A common term with HLAPIs like Mirror, MLAPI, etc. This is referring to a simple object that acts as an adapter between you HLAPI and your LLAPI e.g., Fizzy Steam Transport lets the Mirror HLAPI talk to the SteamNetworking LLAPI for example.
