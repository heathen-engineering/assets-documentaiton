---
description: Play is better together ... sometimes
---

# 🎮 Multiplayer

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what you are seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Designing a game for multiplayer is a whole nother level of design challenge and introduces additional challenges and costs in all other phases of the project in particular multiplayer games typically have a live operations cost meaning the game costs money to run.

Classically their are two major types of multiplayer games though Steam API has given us a hybrid of the two which we will cover here as a 3rd option.  No matter the method of multiplayer its important to make this decision early such that your technical design can account for the challenges before painting you into any corners.

{% hint style="info" %}
Multiplayer concepts have a lot of terms that are very often abused and reused in various contexts. This can make learning about multiplayer a literal hellscape of alphabet soup. Please glance over the Terms article to get a feel for the terms as they are used in our case.
{% endhint %}

## Local

Local multiplayer is where two or more players are playing your game on a single machine. This was the bread and butter of early arcades and consoles and defined several major genres such as fighters, co-ops, etc. In this model 1 instance of the game is running and handles input from two players at once directing that input appropriately for the game in question ... typically each player controls 1 character or some similar clear divide in player authority.

## Online

Online multiplayer is where 2 or more players are playing your game but on two different machines. In this model, a networking session is established between two (or more) machines each of which is running your game and is handling sync of the game state between them. This model has a few variations

### Client

A client is the build of your game e.g. the .exe that runs on the user's machine and presents a visual output (graphics) and handles input (controllers, keyboard, mouse, etc.). In short it is your game as most people know it.

### Server

A server is a build of your game or a process in your game that in a multiplayer session servers 1 or more clients. In general, it processes the code gameplay logic and is the authority of the data state e.g. values and variables that define the state of the game.

#### Listen Server aka Host

A Listen Server is a process that is, it is a Client build that is active as a "server" that other clients can connect to but is also very much a server that is driving a local player game.

#### Dedicated Server aka Game Server

A Dedicated Server is a build of your game that does nothing but server e.g. it is "dedicated" to serving. There is no client to the build only serving.

### Peer to Peer (P2P) Game

{% hint style="info" %}
This term may mean different things in different documents.\
For example, Steam uses "Peer to Peer" to mean communication between 2 or more Steam IDs this could be clients and or servers.\
\
In Unity, Peer to Peer usually refers to a topology where there is no dedicated server, one of the clients generally acts as a "host" being both a server and a client also known as a Listen Server.
{% endhint %}

This is the first and still most frequently used model. In this model, one player connects to another directly with no "server" machine in the middle. The major advantage of this model is that it has little or no live operations cost. The major drawback to this model is it has no "trusted authority" ... that is there is no secured server in the middle so cheating is easily managed by players.

Peer-to-peer can have performance issues depending on the frameworks you use and the nature of your game. For example, MMO using a mesh-style Peer to Peer network is possible but tends to run poorly.&#x20;

### Client/Server Game

In this model, we have a special build of our game called a "Dedicated Server" or "Game Server" sometimes also called a "Headless Build". This server build is typically hosted on a remote machine such as in a cloud service but can be hosted by players (private servers) even on their local computer.&#x20;

A game server build is a special build of your game that strips away features only needed by a client such as rendering. Server builds are thus lighter weight and can run more efficiently on server machines which typically lack graphics cards and similar features.

While it is possible to deploy the server to end users so they can host their local to their computer it is generally more efficient to use a true P2P model. A nice middle ground is to ship the server build and instructions for hosting that server on a VM or through services like G-Portal.

Most typically a Client/Server-based multiplayer game will use a 3rd party LiveOps provider such as PlayFab, Game Lift, etc. who will handle hosting the server, allocating resources, etc. As such most Client / Server games do incur a live operations cost... that is you will have a bill to pay to keep your game running. For this reason, most indies try and avoid this or try to offset the cost with G-portal or similar player hosting options.

## Remote Play

A unique feature of Steam ( for now ) but likely to come to other solutions. This takes a game that was designed for Local multiplayer and uses game streaming technology like Steam's Link to enable a remote player to play with you as if they were on the couch with you.

{% embed url="https://store.steampowered.com/remoteplay" %}

This is simply streaming the game over the Steam client so the other players do not require a copy of the game or even a machine that can run the game, they do however require a network connection suitable for streaming the game over the wire. Implementing this requires [Steam API](../../../toolkit-for-steamworks/steamworks.md) ... and Heathen has you covered there but it's out of scope for this article.

## Network Topology

{% hint style="warning" %}
Head melting?

Then read Star Topology and skip over to Workflow ... \
\
Virtually every indie and small studio game will use P2P Star or Client/Server Star. It is the simplest to manage and typically has the best advantage to draw back comparisons for most games and is what HLAPI's like Mirror, NetCode for GameObjects and FishNetworking assume and do for you.
{% endhint %}

A network topology simply describes how each element on the network talks to the other elements ... e.g. what connections are present and need to be managed for the network to function.

### Star Topology

![](<../../../.gitbook/assets/image (103) (2).png>)

In this structure, all clients connect to a single node, typically a Listen or Dedicated Server. This is the most common topology seen in small-scale multiplayer games. The model does have an upper scale limit in that all clients pass through a single "server". This simplicity is why it's favoured in all games where its scale is not an issue and why it isn't seen typically in large-scale cases such as MMOs which tend to favor a mesh or distributed topology.

### Full Mesh Topology

![](<../../../.gitbook/assets/image (191).png>)

In this structure, every client connects to every other client. This has the advantage that the loss of any one client has no impact on the network state but it also greatly increases the "noise" on the network, that is more network traffic is required to manage the connections and sync objects. This is not a commonly seen structure anymore and is not well supported by most networking tools. Its advantage in the past was that it didn't require a central structure at all however that is not often an issue in modern cases.

### Partial Mesh Topology

![](<../../../.gitbook/assets/image (109).png>)

This structure sometimes also called distributed topology uses a mix of connection patterns. It is the most bespoke topology and would generally mean you are using some very specific tool or have created your own.

Modern MMOs make use of this model where players connect to a "shard" which connects to "world servers" or similar to create a distributed highly scalable topology capable of theoretically handling any number of players.

Specialized "Mega Server" structures use this model where the game server concept will be broken out into multiple nodes, for example, Physics might be handled by one, while AI is handled by another and so on with some controller bringing that back together.

If you are interested in a deep dive, check out the concepts of Spatial OS or "Mega Servers" as you see in MMOs such as Elder Scrolls Online or EVE. It's out of scope for our document here but is an interesting read for the game geek in us all.

## Common Workflow

This will cover the very high-level of a Session-Based "workflow" your player will experience in your game taking them from booting up your game, into a multiplayer session and back to the menu or into another session.

The diagram below shows a simple but typical Session-Based workflow for a game. The two "green" blocks indicate the steps affected by networking, this should help you understand that networking is a relatively tiny part of a multiplayer game in terms of user experience ( UX ) features and systems.

![Simplified multiplayer game loop](<../../../.gitbook/assets/image (98) (2).png>)

You'll also notice the simplicity, many tools or guides tend to get lost in the weeds with multiple rooms or lobbies or session states.

In reality, any multiplayer workflow can be broken down into just 2 parts, Discovery and Gameplay.

### Discovery

This is where you find whatever it is you want to connect to, this could be a friend inviting you, you might browse through a list of options or you could perform some smart query to find a match that suits your arguments.

There are many ways to accomplish this, below are just a few common ones (not an exhaustive list)

* Lobby\
  Think of it like a chat room that people can search for and where players can agree on what they want to play together before spinning up a game session
  * Quick Match / PUG\
    A type of lobby where you search for a specific type of game session and join the best match, you automatically create a matching lobby and wait for others to fill in also called a PUG (Pick up Group)
  * Party\
    This is where the player invites specific players directly into a lobby, they may then perform a Quick Match finding an existing session that can accommodate the whole party or creating a new lobby to suit. It's also possible to simply use this party as the session group without joining non-party players.
* Drop-in/Drop-out\
  This is where you start a session first and invite or otherwise make it possible for specific players to join or leave at any time ... common in classic ARPGs (Dungeon Crawlers). This could use Lobby or Browsers to help the session be discovered ... what differentiates it from other options is in this case the Session is created first, then you make it discoverable whereas otherwise you would discover the players to play with and then when everyone was ready a session would be created.
* Game Server Browser\
  This is where you query to see all available (valid) sessions (servers) that you might join and play on. Not often seen in modern game dev any more but still an option popular in a few specific use cases such as Survival games. SErvers in this case are usually Dedicated Servers but the model can be done with Listen Servers by using a lobby system for searching although this would have some limitations depending on your lobby system.

### Gameplay

This is the game, where the players are playing with each other. You can generally describe multiplayer gameplay in one of two ways

#### Session Based

In a session-based gameplay system the "game world" only exists when there is someone to play it. This is the most common form of multiplayer by far and requires the first player to join to "Allocate" the Gameplay Session. How this is done will depend on your design and tooling but in general, a player will start up a server (aka Host), configure the session to match the type of game desired, spawn in required bits and start-up processes and then when the session is ready to receive, make others aware that the session is ready for connections.

#### Persistent

Only seen in MMOs and even small-scale MMOs will use a Session-based model with an automatic allocation process to cut down on overhead. What denotes a persistent setup isn't the persistence of data, you can persist data even in a session-based system, it is persistent because the server is always present so the game doesn't need to discover it, it can simply assume that "shard" or "world" is there and ready to connect.

## Concepts

### Live Operations

Sometimes called "Live Services" or "Backend Services" these are features and functions that you can add to your design but are not generally part of the game proper. That is these services are housed outside of your game and are accessed via some interface. Live Ops is a very broad subject and will have a dedicated sub-article but the following are a few common features of the topic.

* Authentication
* Cloud Save
* Community Marketplace
* Discovery
* Guilds, Groups, Clans, or other player organization management
* Inventory
* Leaderboards
* Matchmaking
* Micro Transaction / Item Shop ( usually a part of an Inventory system )
* Player Stats & Achievements
