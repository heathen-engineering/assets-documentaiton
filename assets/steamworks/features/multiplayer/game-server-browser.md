---
description: Browse and join listed game servers.
---

# Steam Game Server

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

The Steam Game Server concept is offten confused when you first start looking into Steam and its related tools, interfaces and services.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/multiplayer/game_servers" %}

In the most basic since when we (or anyone) says "Steam Game Server" also shortened as SGS what they mean is a game server that initializes the Steam API with a Steam Game Server configuration. by doing so the SGS can be browsed for through tools like Steam's Game Server Browser and it can leverage key features of the Steam API directly.

## What can it do?

### Networking

{% hint style="warning" %}
Heathen does not provide networking (HLAPI) tools.

You will need to use a tool like Mirror, MLAPI or FishNetworking, etc. as your networking high level interface.



Heathen provides access to Steam APIs and does so in a standardized way such that each of the afore mentioned provider's Steam Transports work with Heathen's Steamworks assets



To make that clear

There is zero customization needed from Heathen to enable you to work with Steam networking. Simply use Mirror, MLAPI, FishNetworking or any other networking highlevel API that has a Steamworks.NET transport.
{% endhint %}

The main advantage to configuring and initializing the Steam API on a game server is the ability to use Steam Networking interfaces with it. Valve provides several networking interfaces but two of them in particular are relevant for Unity game developers

Steam Networking

{% hint style="success" %}
This is not limited to P2P games despite what some of the API names suggest
{% endhint %}

{% hint style="info" %}
Yes Steam has noted that they would like to deprecate this interface in favor of Steam Networking Sockets. No it has not been removed from the API yet and there is no publicized date for such.



As a point in note Steam API still has old authentication logic from more than a decade ago in it e.g. they are not likely to ever break your game by removing API features.
{% endhint %}

and&#x20;

Steam Networking Sockets

### Authentication

The Steam Authentication tools must be used with SGS if you want Steam Game Server Browser to properly list user counts. The [Authenticaiton](../../api/authentication.md) documentation can provide more details.

### Stats and Achievements Security

Stats and Achievements can be a great way to develop your game's community and can even serve as a progression system, however, its extremally easy for user's to set stats and achievements them selves without your game at all.

Stats and Achievements can be configured such that they can only be set from Game Servers (GS) or Official Game Servers (Offical GS). This provides a layer of security and makes it feasible to use Stats and Achievements for game play impacting or community impacting features.

{% hint style="info" %}
It is not to say you must use SGS for Stats and Achievements only that you must accept that every client based feature will be exploited by your users.
{% endhint %}

### Game Server Browser

Put simply server discovery. Steam Game Servers can be configured to list on Steam's Game Server Browser. This can then be used in or out of game to discover game sessions to play or spectate. See the [Game Server Browser Manager](../../components/game-server-browser-manager.md) document for more information

### Hosting

No

Put simply Valve (Steam) doesn't publicly provide hosting ... yet ...

They have teased that they are looking into it but they are a private company they tease lots of things that never come to pass and sometimes things just come out of the blue and are wonderful.

In short there is no facility at current available to you that we are aware where you can host a game server on Valve's servers.

There are great tools available to you though a few are linked below. We do not sponsor or endorse any of them, this is purely to get you started on your own research

* [PlayFab](https://playfab.com)
* [G-Portal](https://www.g-portal.com)
* [Game Sparks](https://www.gamesparks.com) / [Game Lift](https://aws.amazon.com/gamelift/) / [AWS](https://aws.amazon.com)
* [Multiplay](https://unity.com/products/multiplay)
* [Spatial OS](https://ims.improbable.io/products/spatialos)

## Configuration

To configure a Steam Game Server browser simply set the desired settings in your [Steam Settings](../../objects/steam-settings.md#steamsettings.server) object and build a server build. In particular take note of the [Game Server](../../objects/steam-settings/game-server.md) settings.
