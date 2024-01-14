# Terminology

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what you are seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Client

The client is a term that can mean many things. In general a "client" is a consumer of some service, a game for example as in the executable you run to play the game ... that is a "Game Client" even if there is no network it's still a client. Within a single program such as your game, you may have components that are acting as a "client" to other components that are acting as a "server" This is rather common.

In general networking when we say "Client" we mean that which is connected to a "Server". This gets more complex in P2P where one of the "Clients" is also the "Server" also known as a "Host" or "Listen Server".

## Client / Server

This is a type of network topology that describes a "client" connecting to a "server" Specifically when this term is used it means that a Game Client is connecting to a remote Game Server that is running on some machine somewhere else such as hosted in the cloud. This contrasts with "Peer to Peer".

## Dedicated Server

Properly speaking a dedicated server is a build of your game that doesn't do anything other than server. That is it is not a client, generally doesn't have any rendering or take any direct input from a user. This is also sometimes called a "Game Server" or a "Headless Build"

## Game Loop

The flow the player takes through the game from start to finish and back to start again. You can think of this as the workflow of playing your game to use a more business-style term. Sometimes when we say game loop we actually mean a sub-loop within your game for example "combat loop" might refer to the flow of combat and in the context of a combat article or section might simply be called "the game loop".

## High-Level Application Program Interface ( HLAPI )

A term only really seen in Unity,

Aka a High-Level Application Program Interface … see what we say HLAPI now. When we use this, we are usually referring to a networking tool like Mirror, NetCode for GameObjects, FishNetworking, Mirage, etc. What they do is handle the relationship between your game objects and the network … they tend to refer to the network as LLAPI

## Host

Most commonly this means a "Client" that is acting like a "Server" in a Peer to Peer network session also known as a Listen Server.

## Listen Server

The technically proper term for a "Host" which is a game client that is also acting as a server.

## Low-Level Application Program Interface ( LLAPI )

A term only really seen in Unity

As noted in HLAPI this stands for Low Level Application Program Interface. When you’re talking about tools like Mirror, NetCode, etc. they have a concept of a “transport” that is the part of the system that deals with sending and receiving information and handling connections. The interface that transports is built on … that is a LLAPI. In the case of Steam-based networking solutions that would be SteamNetworking and SteamNetworkingSockets as the LLAPI that is used to create the various Steam Transports.

## Lobby

This term gets abused so very often by the developers of networking APIs making it one of the hardest things to understand when first starting.

{% hint style="danger" %}
A lobby IS NOT a networking feature

The word means (etymologically) that which is before and leads to ... so it comes before you have a network session and leads to it.
{% endhint %}

A lobby is best thought of as a chat room or meeting place. It exists before there is a network session set up at all it is where your players will meet to agree on what kind of network session should be set up. In most cases when the network session comes up and the players join it, they would leave the lobby they had met in and the lobby would cease to exist.

Lobbies can be used for loads of features that have nothing at all to do with networking or even multiplayer. Exactly what you can do with the concept of lobby depends on what tools, APIs and backend services you are using in your game. For example, Steam API has a concept of the lobby that ties into matchmaking, friend groups and so much more. It can be used to form parties/groups with friends, drive simple chats and house per-person metadata.

A similar term Room IS NOT a lobby, it is a strange concept used by some networking systems as a sort of pore mans matchmaking service. It doesn't make any sense if you stop to think about what it is doing. See the entry for "Room" in this article for more information.

## Network Manager ( NM )

This term is most common to Unity

Network Manager, most HLAPIs have a concept of a network manager. This is your game's main point of interaction with the network at least so far as starting and stopping a connection. The NM would be what references the transport or transports you wish to support and shuttles data between the rest of the HLAPI such as Network Behaviours to and from the LLAPI via those transports e.g., Send/Receive

## Peer to Peer

A fairly abused term,\
In the context of Steam such as Valve's documentation on Steam, Peer to Peer usually refers to communications between two Steam IDed entities. These could be users and or servers or even clans and groups. It is not strictly speaking referring to a network topology.

With almost every other usage of the term/phrase,\
This is a type of network topology that describes a "client" connecting to another "client" as opposed to a dedicated server such as one hosted in the cloud. That is a P2P connection involves Clients and a Listen Server and contrasts with the similarly abused term "Client/Server" which refers to Clients and a Dedicated Server.

## Room

{% hint style="info" %}
This is a messy term with little value so we avoid using it.
{% endhint %}

This can mean a few things but when it is your HLAPI or your network service provider talking about it ... this is a concept that needs to go die in a hole somewhere.&#x20;

### Network API Concept

What this is, is a network connection to an assumed point aka the "room". It is used by a few tools as a sort of pore man's discovery system or as a pore man's matchmaking system.&#x20;

{% hint style="warning" %}
In my opinion ... which I am sure will irritate many networking API authors

Networking API's often have the miss notion that they are somehow the foundation of the system and they tend to try and ham fist in features a networking API has no business messing with. Common offending systems include but are not limited to

* Scene Management ( part of many Network Managers )
* Matchmaking ( Rooms )&#x20;
* Discovery ( Rooms )
{% endhint %}

### Game Design Concept

In game design when you hear developers talk about a "room" they are either talking about

A lobby; e.g. the point before the network session starts where players meet and decide the rules of the session they will play together.

or

The network session, e.g. The game "room" where players are playing together is sometimes also called a Session, Shard, World, Instance, etc.&#x20;

## Server

( Also ) often abused:

In its simplest form a "server" is anything that serves other things. For example, GitBook is a web server, that serves your browser with HTML content enabling you to read this article.

A computer running a server operating system used to serve other computers with various services is also called a server

A Unity session that is being connected to other Unity sessions to serve them game state information is a game server

A Lobby however is not a server, browsing for lobbies is not a way to make a server list. Server discovery is a separate concept.

## Transport

A common term with HLAPIs like Mirror, MLAPI, etc. This is referring to a simple object that acts as an adapter between your HLAPI and your LLAPI e.g., Fizzy Steam Transport lets the Mirror HLAPI talk to the SteamNetworking LLAPI for example.
