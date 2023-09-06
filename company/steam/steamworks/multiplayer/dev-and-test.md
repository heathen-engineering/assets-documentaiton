---
description: Development and Testing setup
---

# 🧪 Dev and Test

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

This article will cover some common concepts when setting up your project and "rigs" for development and testing.

### TL;DR

{% hint style="info" %}
In short design and early dev should be done with your HLAPIs out of the box transport and without need of a lobby or other matchmaking tool.
{% endhint %}

You do not start with SteamNetworkingSockets transport and a fully fleshed-out lobby UI. \
You start with your HLAPI of choice sample scene and get your concept working there first.

This will identify what you need to make your game possible with that tool e.g. what data is needed to start the session, what objects have to exist and when.

Once you know the required data and have your network architecture designed and implemented and working with your HLAPI's out of the box transport ... then and only then would you integrate with your game. That is now you swap over to using a Steam-based transport, now you start constructing your lobby UI, etc.\
\
Trying to do it backwards will have you rewriting/creating the same things over and over. You cannot know what your lobby needs to gather or do before you have done your network architecture and have it working ... and you cannot get that until you have functional design vaguely working in the HLAPI you choose.

## Dev Phases

Here we outline common phases seen when creating a multiplayer game or feature in a game.

### Functional Design

{% hint style="info" %}
Smoke and Mirrors ... make it at least "appear" to work as intended.\
This phase would be bare bones and wouldn't bother working with Steam, specific transports or even real game assets in most cases.\
\
This is little more than a mod to the sample scenes of HLAPI tool you choose to emulate vaguely what you think your game should feel like.
{% endhint %}

In this phase, you simply make your game loop "theoretically" work with your chosen networking tool. Typically this would be done during the grey box phase of development using the HLAPI or networking tools of your choice and wouldn't have anything at all to do with Steam API just yet.

The focus here is to understand&#x20;

1. Does your current game design even work in multiplayer
2. Does your chosen HLAPI / tool support your functional requirements

This is usually done in a standalone sandbox scene using simple cubes and other primitives and leveraging out-of-the-box samples from the HLAPI / network tool itself.

The output of this phase informs what features your multiplayer will and won't have and roughly how they will work. Importantly this lets you know what network behaviours you will need to design in the next phase and roughly what their functional requirements will be for example:

You will almost certainly need a "UserNetworkController" to be spawned for each connected player. You will probably want that to register itself on some common singleton or static object for easy access by other systems and you will probably want that to have details about that player unique to your game e.g. character selection, team, loadout, etc.

### Technical Implementation

{% hint style="info" %}
Network Architecture ... this is where you create your multiplayer game.\
This wouldn't bother with lobbies, specific transports, etc. It is more about creating out-of-the-boxunique behaviours and scripts and understanding what data your multiplayer session is working with and what it requires to be started.
{% endhint %}

This phase is about making the "Smoke and Mirrors" you set up in the prior phase "real" that is replacing the hacked-in samples and ham-fisted bits with properly designed behaviours. You would do this now not later as through the technical design you will identify the requirements your network architecture has on the wider game.&#x20;

For example in a game where your players choose a character and load out ... that tells you your menu or lobby system will need to gather data from the player before there is a network session and make it available to the network on start-up.

The output of this phase informs the requirements of your UX and wider game systems to enable your multiplayer session to function as required. You will use the results of this design for your discovery tooling, matchmaking, authentication process, fault recovery and more.

### Integration

{% hint style="info" %}
This is where you connect all your work so far to the game proper. \
Now we create a lobby system, we use whichever transport you have settled on and we start to see a "real" game take shape.
{% endhint %}

This is the point where you integrate the multilayer features you have designed and implemented with your wider game. For example, here you may design and implement a lobby system that gathers player character selection and loadout and deals with with user authentication to set up a P2P session.

The specifics of what you do here will depend entirely on the nature of your game and the results of your technical implementation.&#x20;

## Testing

You should be testing as you go and how you test will depend on which phase you are in.

### Design & implementation

During Functional Design and Technical Implementation, you use out-of-the-box, tools from your HLAPI of choice. So to test simply follow the instructions of your HLAPI in regards to running its sample scenes. This usually means making a build, starting it, having it start a session; next running the editor simulation and connecting it to that session.

In this phase having 1 dev use 1 machine to test the client and host/server is easily doable. Keep in mind this is not "network testing" this is design testing, and no network is involved yet. You simply use a primitive transport like TCP or UDP to fake a connection to yourself so you can test ideas and functions using out-of-the-box behaviours.

### Integration

The final phase is integration where you connect your completed and working network architecture to your wider game. Now is when you would switch your transport over to whatever transport you will use in production likely a SteamNetworkingSockets-based transport. You would also set up whatever "discovery" or "matchmaking" tool you want to use ... likely based on Steam Lobby.

With these two things done you can no longer fake a connection, you now require two machines with two unique Steam accounts both licensed for the game to test. At this point, you are performing "real" network testing. That is data is travelling over the network subject to latency and all that goes with it.
