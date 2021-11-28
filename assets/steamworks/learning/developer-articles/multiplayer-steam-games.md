# Multiplayer Steam Games

## Introduction

### Who am I?

James McGhee CEO and founder of Heathen, author of all of Heathen’s coded assets and a contributor to Steamworks.NET, Mirror’s FizzySteamTransport, MLAPI’s Steam Transport and really anything else I can help with.

### What do I know?

Only what I’ve learned, and I’m here to share that; not dictate what you should do. As to my experience I have worked on Unity creating games and related apps and technology for nearly a decade at the time of this writing. Aside from Unity specific work I am a software engineer with 20-ish years’ experience in the enterprise software engineering sector. I have, I think a good mix of experiences including all aspects of development across a very wide range of applications and industries and I try to bring to bring that to the tools I create and information I share.

### What is this?

Just me as an individual sharing what I have learned with my fellow developers. This is not written as an expert’s guide, an essay on best practices or any such formal thing. It is a effectively a brain dump of things I have learned that hopefully will help you going forward.

## Overview

Let’s start by saying this here:

Creating a game is hard work, creating a multiplayer game is extra hard work, creating a massively multiplayer game is … well you get the idea. If this is your first game or even 5th game, I would personally recommend spending some more time creating smaller stand alone projects you can get done from start to finish. With that out of the way let’s get started.

## Terminology

This is just a list of terms I will use in this article, they are not necessarily the right terms or standard terms, etc. again this is just me sharing info and this section is just meant to help you translate my dribble.

### Game Loop

The flow the player takes through the game from start to finish and back to start again. You can think of this as the workflow of playing your game to use a more business style term.

### HLAPI

Aka a High-Level Application Program Interface … see what we say HLAPI now. When we use this, we are usually referring to a networking tool like Mirror, MLAPI, FishNetworking, Mirage, etc. they are APIs but not all of it. What they do is handle the relationship between your game objects and the network … they tend to refer to the network as LLAPI

### LLAPI

As noted in HLAPI this stands for Low Level Application Program Interface. When you’re talking about tools like Mirror, MLAPI, etc. they have a concept of a “transport” that is the part of the system that deals with sending and receiving information and handling connections. The interface that transports is built on … that is a LLAPI. In the case of Steam based networking solutions that would be SteamNetworking and SteamNetworkingSockets as the LLAPI that is used to create the various Steam Transports.

### NM

Network Manager, most HLAPIs have a concept of a network manager. This is your games main point of interaction with the network at least so far as starting and stopping a connection. The NM would be what references the transport or transports you wish to support and shuttles data between the rest of the HLAPI such as Network Behaviours to and from the LLAPI via those transports e.g., Send/Receive

### Transport

Again, a common term with HLAPIs like Mirror, MLAPI, etc. This is referring to a simple object that acts as an adapter between you HLAPI and your LLAPI e.g., Fizzy Steam Transport lets the Mirror HLAPI talk to the SteamNetworking LLAPI

## Preparing your Project

### Step 1

Select the proper Unity Version.

We have a [whole article on this](../../../../company/concepts/unity-release-version.md), long story short you should aim to release your project on the most recent LTS available from Unity.

### Step 2

Installing requirements

Pick a HLAPI you like and go with it, I will use Mirror in the rest of this not because its best or my favorite, etc. but because it’s the most uNET like which many of you will know from past projects and is still quite like all the others.

For all there hemming and hawing about how there HLAPI is the best-ist ever, most are so strikingly similar that if you’re bumping up against there differences in a way that hurts your game you might want to consider a custom solution more specific to your game … its easier than you might think. We might cover that in a later topic.

Aside from your HLAPI of choice you will need of course

Steamworks.NET

Heathen’s Steamworks (I suggest Complete, but Foundation might do you)

[UX Complete](../../../ux/) can be a big help as well if you want to [manager your scenes directly](../../../ux/components/scenes-manager.md) though some HLAPI NMs do some crude scene management.

### Step 3

Setting up your Steam project. There are other articles in this section that go over working with Steam API so read those.

As to general project architecture check out [these articles](../../../../company/concepts/bootstrap-scene.md), concepts such as bootstrap scenes can be a big help in really most projects.

{% hint style="info" %}
Pro Tip

Keep your product project clean and light.



I personally like to set up 2 projects with each "game project" .

1\) The "production" project will be keep clean and I will only ever install just what it needs that is when I import an asset I will exclude its prefabs, samples, documents, etc. keeping only the functional parts I need to use.



2\) The "sandbox" project this is where I pull things in as they where defined by there authors and where I play with my own code and assets making a right mess but designing and iterating quickly



When something is fit for production I simply export it from Sandbox and bring it into Production. This lets me be a messy boy as I design and experiment which I love to do while also keeping the bloat out of the production product.
{% endhint %}

## Key Concepts

### Game Scene

You will have a scene that is used during your gameplay. Rather this is loaded by a host preparing a game for connections or a game server depends on your needs and game. What you do want to do is keep this scene light and flexible.

Many HLAPIs are able to define Network Objects as part of a scene and initialize them on start up. This can be handy but it can also make debugging a nightmare. Consider at least keeping the scene its self free of any networking concepts then have the server or host as the case may be spawn in the required items as they configure the environment for play.

This may sound like extra work but it keeps the scene small, flexible so you can easily use 1 scene for many session types and makes debugging and troubleshooting vastly easier as network only gets involved when you say so.

### Scene Management

Mirror at least and MLAPI I think have a very crude scene management feature.&#x20;

You don't need this, in my experience it only serves to make things more complicated. In reality the network doesn't care what scene is loaded or not or what is active or not. Unity does as that defines what GameObjects are loaded where and which environment settings are active.

We find it best to have the client handle load and unload of scenes as makes since for them. A lot of this comes from the realization that Unity handles multi-scene nicely and that a scene doesn't need to represent a physical area in your game so letting a network system which is driven by network visibility drive that makes no since.

[See this article for more](../../../../company/concepts/multi-scene-architecture.md)

See [UX Complete](../../../ux/components/scenes-manager.md) for tools that can help you really leverage the power of Unity's scene system

### Player Controller (PC)

Keep your PC simple, think of the PC a bit like you might think of Unity's Event System or Input System.&#x20;

It probably shouldn't be a visual element in your game, rather its there to capture the inputs of the player it represents and sync that over the network and to notify all other players as that input changes.

It makes since to store player specific values on it but player is not character. In most of our use cases our PC is just an IO sync tool with some state info like what team the player is a part of. We have the PC spawn character controllers as required and these character controls define the visuals, sync animations, store character health, level, etc.

### Set Game Server

A feature of Steam's Lobby system. SetGameServer is a method available to you on the [Lobby](../../objects/lobby.md) and through the [Matchmaking ](../../api/matchmaking.md)API. Only the owner of the lobby can call this method.

What it does is when this is called it will cause an event to be raised on all the members of the lobby to notify them that the server's connection information has been set and they can now join to it.

This should be called by the owner of the lobby when the network environment is ready for users to connect to it. E.g. this is called in P2P after the Host has called StartHost and configured the network environment. In Client/Server its called after the owner has allocated a server and configured it.

When this is called the owner can specify a CSteamID representing the steam peer or Steam Game Server.

Users that join the lobby after the event has occured will not get the event raised however they can test if it has already been set via&#x20;

```csharp
if(lobby.HasServer)
{
    NetworkManager.address = lobby.GameServer.id.ToString();
    NetworkManager.StartClient();
}
```

## The Game Loop

So, remember we are not talking about an Update Loop here we are talking about the human experience of starting your game and cycling through it session by session until the player exits your game.

I’ll start with Peer-to-Peer based games and then we can go over the differences with Client Server.

### Peer to Peer

1. Player A starts the game and indicates to your UI that it wants to play a multiplayer match as the host of a session let’s say. This can happen after the player has exhausted a search for an existing game that suits or simply because it wants to be the host that part is up to you.
2.  Player A configures the conditions of the game they want to host e.g., mode, map, etc. This information will get stored on a Steam Lobby as metadata and used in the matchmaking process e.g., others searching for a game can filter on this information.

    When the player creates the game, they will likely do so as a public lobby and so other players can browse for or quick match on this lobby and join it. As other players roll in the can communicate with each other via the Steam Lobby Chat system to agree on any other terms they need such as what characters each will use or teams, etc. Again, that is specific to your game.
3.  At some point Player A will decide its time to play the game. Player A may want to lock the Steam Lobby so no one else can join that is an option but the main thing is that Player A starts up the network environment e.g.

    Player A calls NM to Start Host and then configures the network environment to suit the desired conditions i.e., loads levels, spawns’ environments, etc.
4.  When Player A is happy that the network environment is ready for use, they will call SetGameServer on the Steam Lobby providing their own ID as the server information. This will notify all other players that the session is ready to connect to and so each other user will handle that event, navigate to the appropriate scene in your game and call StartClient on the NM

    Typically, as players connect to the host/server they will leave the lobby. You can maintain the lobby for the duration of the session if you like such as to enable droping players to come in after session start. Do know though that SetGameServer will only invoke its events once per lobby so in short, a Steam Lobby represents a single game session.
5. At some point the session will come to an end. Many games will show a post session UI and here is a good place to invite the players to join a new lobby together such that they might play a second or third session together. You can decide if you keep the same host or not that is up to you. The point is you offer them to join a new lobby or to return to menu or some similar “hay its over now go home”

### Client Server

Really a Client Server game is very much the same as Peer to Peer the only difference is in step 3 and 4. The lobby owner in a Client Server game will need to do something to set up a new server. For example, you could use PlayFab and request the allocation of a new GameServer. PlayFab will respond with connection information, and you can use that on the SetGameServer call

Note that Game Servers can be configured as “Steam Game Servers” that is they can log on to steam as a server for your game and will get a CSteamID that be used with SteamNetworking and SteamNetworkingSockets. See the Steam Game Server documentation for more information on SGS.
