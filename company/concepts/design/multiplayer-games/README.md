# 🎮 Multiplayer Games

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Designing a game for multiplayer is a whole nother level of design challenge and introduces additional challenges and costs in all other phases of the project in particular multiplayer games typically have a live operations cost meaning the game costs money to run.

Classically their are two major types of multiplayer game though Steam API has given us a hybrid of the two which we will cover here as a 3rd option.  No matter the method of multiplayer its important to make this decision early such that your technical design can account for the challenges before painting you into any corners.

{% hint style="info" %}
Multiplayer concepts have a lot of terms that are very often abused and reused in various contexts. This can make learning about multiplayer a literal hell scape of alphabet soup. Please glance over the Terms article to get a feel for the terms as they are used in our case.
{% endhint %}

## Local

Local multiplayer is where 2 or more players are playing your game on a single machine. This was the bread and butter of early arcade and consoles and defined several major genre such as fighters, co-ops, etc. In this model 1 instance of the game is running and handles input from two players at once directing that input appropriately for the game in question ... typically each player controls 1 character or some similar clear divide in player authority.

## Online

Online multiplayer is where 2 or more players are playing your game but on two different machines. In this model a networking session is established between the two (or more) machines each of which is running your game and is handling sync of the game state between them. This model has a few variations

### Peer to Peer (P2P)

This is the first and still most frequently used model. In this model one player connects to another directly with no "server" machine in the middle. The major advantage of this model is that it has little or no live operations cost. The major draw back to this model is it has no "trusted authority" ... that is there is no secured server in the middle so cheating is easily managed by players.

Peer to peer can have performance issues depending on the frameworks you use and the nature of your game. For example a MMO using a mesh style Peer to Peer network is possible but tends to run poorly.&#x20;

### Client / Server&#x20;

In this model we have a special build of our game called a Game Server (e.g. Headless build or Dedicated Server build). This server build is typically hosted on a remote machine such as in a cloud service but can be hosted by players (private servers) even on their local computer.&#x20;

A game server build is special build of your game that strips away features only needed by a client such as rendering. Server builds are thus lighter weight and can run more efficiently and on server machines which typically lack graphics cards and similar features.

While it is possible to deploy the server to end users so they can host their own local to their computer its generally more efficient to use a true P2P model. A nice middle ground is to ship the server build and instructions for hosting that server on a VM or through services like G-Portal.

Most typically a Client / Server based multiplayer game will use a 3rd party LiveOps provider such as PlayFab, Game Lift, etc. who will handle hosting the server, allocating resources, etc. As such most Client / Server games do incur a live operations cost... that is you will have a bill to pay to keep your game running. For this reason most indies try and avoid this or try to offset the cost with G-portal or similar player hosting options.

## Remote Play

A unique feature of Steam ( for now ) but likely to come to other solutions. This takes a game that was designed for Local multiplayer and uses game streaming technology like Steam's Link to enable a remote player to play with you as if they where on the couch with you.

{% embed url="https://store.steampowered.com/remoteplay" %}

This is simply streaming the game over the Steam client so the other player's do not require a copy of the game or even a machine that can run the game, they do however require a network connection suitable for streaming the game over the wire. Implementing this requires [Steam API](../../../../assets/steamworks/) ... and Heathen has you covered there but its out of scope for this article.

## Network Topology

{% hint style="warning" %}
Head melting?

Then read Star Topology and skip over to Workflow ... \
\
Virtually every indie and small studio game will use P2P Star or Client/Server Star. Its the simplest to manage and typically has the best advantage to draw back comparison for most games and is what HLAPI's like Mirror, NetCode for GameObjects and FishNetworking assume and do for you.
{% endhint %}

A network topology simply describes how each element on the network talks to the other elements ... e.g. what connections are present and need be managed for the network to function. If your using any of the typical HLAPIs available for Unity then your using a Star Topology, if your looking to create a very large scale multiplayer game such as an MMO or mass shooter then you will likely need to consider some of the other options. Their are providers and tools out there to help you with this and to even handle all the complexity for you in a manner similar to a typical Unity HLAPI solution. See the Tools article for more information.

### Star Topology

![](<../../../../.gitbook/assets/image (109).png>)

In this model one of the players acts as the "host" and all other players connect to this host. The host in effect acts like a "server". This model has the advantage of a simple connection graph and is the one most HLAPI's assume you are using. It has the disadvantage that if the host is lost, the whole session is lost. In addition the host is the "server" for all other peers meaning that host client is under considerably more stress than other's. While there are ways to compensate for this drawback that is beyond the scope of this section.

### Full Mesh Topology

![](<../../../../.gitbook/assets/image (112).png>)

In this model every client connects to every other client. This has the advantage that the loss of any 1 client has no impact on the network state but it also greatly increases the "noise" on the network, that is more network traffic is required to manage the connections and sync objects. Most HLAPIs have no facility for this model. This model is rare in game development but in games with a small number of participants it can be a useful P2P solution due to its high redundancy which can be used to combat cheating and of course tolerate network drops.

### Partial Mesh Topology

![](<../../../../.gitbook/assets/image (99).png>)

In this model each client connects to one or more other clients but not all other clients. This does appear in a few games usually team based shooters where there is a server involved but only minimally and where peer connections are used for much of the traffic. This is again not something you would see in a typical HLAPI and is fairly complex to manage but does offer advantages in load balancing and offers some degree of redundancy.

If your interested in a deep dive, checkout the concepts of Spatial OS or "Mega Servers" like you see in MMOs such as Elder Scrolls Online or EVE. Its out of scope for our document here but is an interest read for the supper geek.

## Workflow

This will cover the very high level "workflow" your player will experience in your game taking you them from booting up your game, into a multiplayer session and back to menu or into another session.

The diagram below shows a simple by typical workflow for a game. The two "green" blocks indicate the steps effected by networking, this should help you understand that networking is a relatively tiny part of a multiplayer game in terms of user experience ( UX ) features and systems.

![Simplified multiplayer game loop](<../../../../.gitbook/assets/image (101).png>)

## Concepts

### Discovery

{% hint style="danger" %}
This should not be a networking feature, its a service feature.
{% endhint %}

The concept of discovery is that for some games the player needs to "Discover" game sessions available to be played. In modern gaming discovery is fairly rare with most modern games choosing to go with matchmaking or other "transparent" solutions.&#x20;

When discovery is used it is most commonly with Client / Server games where the servers are simi-persistent such as survival games. The most appropriate way to handle discovery is through a backend service provider. For example Steam API provides you with a "Game Server Browser" which can handle matchmaking or be used to "browse" available servers e.g. is a discovery tool. G-Portal, Play Fab and other backend service options all provide there own solution to server discovery and while this concept leads to a multiplayer session its not a networking feature.&#x20;

### Matchmaking

{% hint style="danger" %}
This should not be a networking feature, its a service feature.
{% endhint %}

The concept is that your game should be able to search for other players looking for a session or even other sessions currently running in some filtered manner such that the ideal "match" is returned.
