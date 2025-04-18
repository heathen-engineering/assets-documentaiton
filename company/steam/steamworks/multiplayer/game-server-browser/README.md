---
description: Browse and join listed game servers.
---

# 💁 Steam Game Server

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Steam Game Server concept is often confusing when you first start looking into Steam and its related tools, interfaces and services.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/multiplayer/game_servers" %}

{% hint style="danger" %}
Please click the link shown above or again here and read Steam's documentation on the subject.

[https://partner.steamgames.com/doc/features/multiplayer/game\_servers](https://partner.steamgames.com/doc/features/multiplayer/game_servers)
{% endhint %}

In the most basic sense when we (or anyone) says "Steam Game Server" also shortened as SGS what they mean is a game server that initializes the Steam API with a Steam Game Server configuration. By doing so the SGS can be browsed for through tools like Steam's Game Server Browser and it can leverage key features of the Steam API directly.

## What can it do?

### Networking

{% hint style="warning" %}
Heathen does not provide networking (HLAPI) tools.

You will need to use a tool like Mirror, MLAPI, FishNetworking, etc. as your networking high-level interface.



Heathen provides access to Steam APIs and does so in a standardized way such that each of the aforementioned provider's Steam Transports works with Heathen's Steamworks assets



To make that clear

There is zero customization needed from Heathen to enable you to work with Steam networking. Simply use Mirror, MLAPI, FishNetworking or any other networking high-level API that has a Steamworks.NET transport.
{% endhint %}

The main advantage to configuring and initializing the Steam API on a game server is the ability to use Steam Networking interfaces with it. Valve provides several networking interfaces but the main one you should be looking at is the Steam Networking Sockets APIs

{% hint style="success" %}
This is not limited to P2P games despite what some of the API names suggest
{% endhint %}

### Authentication

The Steam Authentication tools must be used with SGS if you want the Steam Game Server Browser to properly list user counts. The [Authentication](../../../../../old-toolkit-for-steamworks/unity/api-extensions/authentication.md) documentation can provide more details.

### Stats and Achievements Security

Stats and Achievements can be a great way to develop your game's community and can even serve as a progression system, however, it's extremely easy for users to set stats and achievements themselves without your game at all.

Stats and Achievements can be configured such that they can only be set from Game Servers (GS) or Official Game Servers (Official GS). This provides a layer of security and makes it feasible to use Stats and Achievements for gameplay-impacting or community-impacting features.

{% hint style="info" %}
It is not to say you must use SGS for Stats and Achievements only that you must accept that every client-based feature will be exploited by your users.
{% endhint %}

### Game Server Browser

Put simply server discovery. Steam Game Servers can be configured to list on Steam's Game Server Browser. This can then be used in or out of the game to discover game sessions to play or spectate. See the [Game Server Browser Manager](../../../../../old-toolkit-for-steamworks/unity/objects/components/game-server-browser-manager.md) document for more information.

### Hosting

No

Put simply Valve (Steam) doesn't publicly provide hosting ... yet ...

They have teased that they are looking into it but they are a private company they tease lots of things that never come to pass and sometimes things just come out of the blue and are wonderful.

In short, there is no facility at current available to you that we are aware of where you can host a game server on Valve's servers.

There are great tools available to you though a few are linked below. We do not sponsor or endorse any of them, this is purely to get you started on your own research

* [PlayFab](https://playfab.com/)
* [G-Portal](https://www.g-portal.com/)
* [Game Sparks](https://www.gamesparks.com/) / [Game Lift](https://aws.amazon.com/gamelift/) / [AWS](https://aws.amazon.com/)
* [Multiplay](https://unity.com/products/multiplay)
* [Spatial OS](https://ims.improbable.io/products/spatialos)

## Configuration

To configure a Steam Game Server browser simply set the desired settings in your [Steam Settings](../../../../../old-toolkit-for-steamworks/unity/objects/classes/steam-settings/#steamsettings.server) object and build a server build. In particular take note of the [Game Server](../../../../../old-toolkit-for-steamworks/unity/objects/classes/steam-settings/game-server.md) settings.

## Hosting

{% hint style="warning" %}
At this time Valve (they build Steam) does not offer hosting you will have to provide for that yourself.
{% endhint %}

### Player Hosted

This means that you ship your server build and let players host them, themselves. It was a popular method in the past and many games still allow for it especially if you want to foster a LAN community.

### Bespoke

Abuse of the term but what is meant here is a hosting service provider. These are usually used to let your player host servers. Minecraft, Ark, and Conan Exiles, this is a popular model in survival games.

Look for providers like [GPortal](https://www.g-portal.com/) to help with this.

### Backend Service Provider

The new traditional method, using a backend service provider, most if not all of these offer hosting of some sort along with other services.

Look for providers like [PlayFab](https://playfab.com/), [GameSparks ](https://www.gamesparks.com/)and [Multiplay](https://unity.com/products/multiplay)

### Proprietary

There are some options that offer great advantages but those are proprietary systems so moving off of them is not really possible at least not without a lot of work. We would only recommend you consider these if your game REALLY needs the advantage they offer and you are happy to marry your game to their offerings.

Look at providers like [Improbable](https://ims.improbable.io/)

### DIY

Do it yourself, not recommended for ... well most people and even large organizations. It is exceedingly difficult to host a live service game of any kind without a lot of money and experience and 24-hour-a-day staff.&#x20;

That said it is an option and you can offset some of the cost by using basic hosting services like [Azure](https://azure.microsoft.com/), [AWS](https://aws.amazon.com/), etc.
