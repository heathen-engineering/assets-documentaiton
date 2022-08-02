---
description: Information on available tools and services for your next multiplayer project
---

# Choosing a Tech Stack: Networking

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article is here simply to highlight the options available to you when thinking about the networking and backend services of your next game. This assumes your game is going to be released on Steam and will be using Steamworks Complete to some extent.

{% hint style="info" %}
Heathen is not affiliated or partnered in away with any of the technologies listed below. We have used or reviewed for internal use every technology mentioned here.

\
The purpose of this article is simply to highlight your options and our thoughts on each to jump start your own research. You should still do your own research and choose the stack that suits you, your team and your project best.
{% endhint %}

## Terms

To keep it clear I will define any tech jargon we use in this article here. These definitions are how we use them, in general they are industry standard but the fact is especially networking "standard" is more of a guideline than a rule really or so many would treat it.

### Backend Service

Part of live operations this is the set of features and services that provide for your "under the hood" services like matchmaking, server allocation, ranking, security, etc. In many articles "Backend Service" and "Live Operations" are used interchangeably. When they are used to gather "Live Ops" generally refers to the whole suit of services including the customer facing ones like account management where backend service refers specifically to those "behind the curtain" services e.g. not customer facing.

### HLAPI

High Level Application Program Interface ... in this context we are referring to part of a network technology stack in particular the part that you as a game programmer will be working with directly in your game code. This part deals with the serialization of game data preparing it for transmission via the "LLAPI" and this part takes data provided by the LLAPI and de-serialises it syncing your game objects accordingly.

### Live Operations

This is an old term made buzz word again here recently. Live Ops, refers to the systems, services and processes of operating a live system. In games in particular it refers to those systems and services like Steam, PlayFab, etc. that deal with accounts, stats, leaderboards or really any thing else that might be part of that "live service" experience. but also refers to more mundane things like server hosting, content deliver, etc.

### Live Service

In the world of game we usually mean this to be a game that has a part or is wholly dependent on its Live Ops service i.e. the player must log in to play or at least to play this part of the game.

### LLAPI

Low Level Application Program Interface ... in this context we are referring to part of a network technology stack in particular the part that your transport interacts with to read packets to be sent and to write packets it received. The LLAPI works with the "Transport" and the "HLAPI" ... in many documents "LLAPI" is used interchangeably with "Transport" when the two terms are used together "Transport" refers to the class that implements the "LLAPI" so for example the FizzySteamTransport implaments the SteamNetworking API

### Transport

In this context we are referring to part of a networking tech stack that deals with the transmission of data. Many networking stacks are transport agnostic ... meaning you can swap in and out multiple transports. For example Mirror, NetCode and FishNetworking all use such a transport system so you can even at run time swap between TCP, UDP, KCP and SteamNetworking ... why usually to support multi-platform. The real point is the transport is separate from the "HLAPI"

## Our Preference

This is wholly our own opinion but for the TL:DR out there (there are lots of you) this is what we feel is the best option and why.

### Peer to Peer Games

Steamworks Networking APIs + ([FishNetworking ](https://github.com/FirstGearGames/FishNet)or [NetCode ](https://github.com/Unity-Technologies/com.unity.netcode.gameobjects)or [Mirror](https://github.com/vis2k/Mirror))\
In short Steamworks is the weapon of choice for LLAPI and so any HLAPI that directly supports it e.g. [FishNetworking](https://github.com/FirstGearGames/FishNet), [NetCode for GameObjects](https://github.com/Unity-Technologies/com.unity.netcode.gameobjects) and [Mirror ](https://github.com/vis2k/Mirror)are all viable options. Personally our openion is the tech difference in terms of capability differences between the 3 is negligible so pick the one whose community you vibe with most. If your game's networking is more complex perhaps dig deeper into the unique strengths and weaknesses of each.

Why?

Steamworks SteamNetworking and SteamNetworkingSockets are the supperior options for LLAPI full stop. They do not require IP/Port, they run over Valve's dedicated network edge to edge and they can exploit the features of Steam's social network for discovery, matchmaking and more.&#x20;

Thus anything that supports it directly is the better option. This means Photon is redundant as it doesn't offer you anything that Steamworks doesn't already have ... and for free ... and at a higher level of quality.

### Client Server&#x20;

Steamworks Networking APIs + ([FishNetworking ](https://github.com/FirstGearGames/FishNet)or [NetCode ](https://github.com/Unity-Technologies/com.unity.netcode.gameobjects)or [Mirror](https://github.com/vis2k/Mirror)) + ([PlayFab ](https://playfab.com/)or [GameLift](https://aws.amazon.com/gamelift/) or GPortal)

As with the above Steamworks Networking APIs are hands down the bet way to talk between two Steam gamers or a Steam Gamer and a Steam Game Server … so the only thing we need to add to make this Client Server … is a hosting provider.

There are 3 main options here

[PlayFab](https://playfab.com/)\
Microsoft Azure based able to scale well beyond what others can do and drives some of the biggest live ops based games in the industry. The entry point is free and the operations cost low. It has tutorials and instructions for use with Steam and Mirror, etc. so on boarding is easy and its has a native integration with Steam API making it easier to leverage advanced features like trusted stats, achievements and leaderboard, Steam MTX, etc.

[GameLift](https://aws.amazon.com/gamelift/)\
Second place goes to Amazons GameLift aka AWS though technically GameLift is built on AWS … anyway solid option only second place by a tiny margin based on its costs and being a bit clunky to use compared to PlayFab.

[GPortal](https://www.g-portal.com/business/)\
Finally this is a unique option so not really 3rd place rather this is the option to go with if you don't need "backend services" and you simply need a solid host for your servers rather that is player ran servers or official servers. GPortal is an old classic style of game server hosting provider which can save you the cost and operations overhead by making it trivial for your gamers to pay to host there own servers.

## Technology

### [FishNetworking](https://github.com/FirstGearGames/FishNet)

FishNetworking is a newer HLAPI compared to the other options and is very similar sporting that same uNET style structure. As always this also has a ready to use [Steam transport](https://github.com/FirstGearGames/FishySteamworks).

With this and similar HLAPI there isn't a ton to say that isn't available at the links above, we consider this a viable option and in many cases the best option for your HLAPI.

### [GameLift](https://aws.amazon.com/gamelift/)

From Amazon and built on the AWS platform GameLift is very similar to PlayFab in that its a full service Live Operations solution which pairs nicely with other tools or can function as the core of your stack as noted in the our preference section above.

### [G-Portal](https://www.g-portal.com/business/)

An often overlooked solution by indies but quite common with modern Survival games mil sims. G-Portal is a classic style host, that means it is just server hosting nothing more. That makes it easy for you or your gamers to rent servers for your favourite games. You can use G-Portal to set up dedicated Steam Game Servers or you can leave that to your players to do saving you the costs.

While we haven't used it our selves yet we have reviewed it and plan to use it in upcoming projects. You can see it used in games like Conan Exiles where players can easily stand up a server which will be discoverable via Steam Game Server Browsing. So this is really a great tool when you don't need extra backend services such as you get from PlayFab or GameLift and or you want to keep operations cost to zero.

### [Mirror](https://github.com/vis2k/Mirror)

Mirror is or rather started life as a variant of uNET. When Unity abandoned uNET; Mirror picket it up and ran with it. Pretty easy to use and as is most important it has a ready to use [Steam transport](https://github.com/Chykary/FizzySteamworks/).

With this and similar HLAPI there isn't a ton to say that isn't available at the links above, we consider this a viable option and in some cases the best option for your HLAPI.

### [Multiplay](https://unity.com/products/multiplay)

More of a partner really than a technology Multiplay are defiantly big boys in the industry. They do not provide for you HLAPI or LLAPI but they do handle those backend services and operations needs.

### [NetCode for GameObjects](https://github.com/Unity-Technologies/com.unity.netcode.gameobjects)

NetCode the HLAPI formerly known as MLAPI related to uNET now owned by Unity

<img src="../../../../.gitbook/assets/FacepalmGIF.gif" alt="" data-size="original">

While this one's lineage is well laughable to say the least; it also has a [Steam transport](https://github.com/Unity-Technologies/multiplayer-community-contributions/tree/main/Transports/com.community.netcode.transport.steamnetworking).

With this and similar HLAPI there isn't a ton to say that isn't available at the links above, we consider this a viable option and in some cases the best option for your HLAPI.

Why is it funny?

MLAPI was closely related to uNET in form and function … which Unity abandoned and about a year after throwing the baby out with the bathwater … they purchased and rebranded MLAPI. Why Unity didn't either fund Mirror or better yet not throw uNET out and just fix it … cant say.

Oh and MLAPI just in and of its self is a LOL … its a HLAPI the name just adds insult … MLAPI was a concept as well actually Unity has a "MLAPI" concept for its DOTS stack … not a tech but a concept like you have HLAPI and LLAPI … so ya the name of this product was a tragedy as is its history.

### [Photon](https://www.photonengine.com/)

<img src="../../../../.gitbook/assets/NoGodPleaseNoGIF.gif" alt="" data-size="original">

Jokes aside, Photon's claim to fame here is&#x20;

1. Early to market\
   When Photon came on the scene we had RakNet, Steamworks.NET and that was about it in terms of indie frinedly networking bits and neither was a full stack; so for its day ... a god send.
2. One Stop Shop\
   Photon everything all in one ... IMO that is a bad thing but its an easy thing I suppose.&#x20;

Why don't we like it

* Quality of service compared to other options is low
* Feature set compared to other options is low
* Scalability compared to other options is low
* Price is high
* Method of metering price is not indie friendly
* Tech stack is proprietary so switching has a high dev cost

All that said you can use this along side Steamworks.NET but you will not be using Steam's Networking and you will have many redundant services and features.

### [PlayFab](https://playfab.com/)

From Microsoft and built on the Azure platform, PlayFab is a Live Operations provider, it covers all of your backend service needs, hosting and a lot more. It has integrations with Steam and works wonderfully as an add on to any networking stack or as a core component in your networking stack such as seen in our preference section about for the Client Server set up.

### Steam API

If your even reading this you know the value added here but there are a few parts specific to networking beyond simple LLAPI.

All of these features are well documented throughout this Knowledge Base so we wont detail them again here simply point out those features which are commonly used in multilayer experiences and that some may think they need to pay extra to have via a 3rd party provider.

Steam API provides all of these and a lot more for you, for free ... well as part of that 30% they are going to take anyway!

* Authentication
* Matchmaking
* Steam Game Server
* Server Browser
* Valve Anti Cheat
* Steam Micro Transaction (MTX)
* Remote Play
* Parties
* Broadcasting
* Lobbies
* Chats
* Rich Presence
* Stats & Achievements
* Leaderboards
* User Generated Content (aka Workshop)
* Community Hub
* Voice
* Cloud Saves / Remote Storage

### Steam Networking

This is part of the Steam API we simply call it out on its own here to highlight its claim to fame.

Steam Networking Sockets API … this is a LLAPI, it can be used on its own without a HLAPI if your comfortable doing that or you can (and most do) us it with a HLAPI like FishNetworking or Mirror. Steam's Networking APIs are in our opinion the best option for any indie or really any game that is not looking for mutli-platform … and even then with multiplexing … its still the best for your Steam Gamers. Steam Networking is a "LLAPI" in the context of our terms so its not the whole stack ... just the most important part.

You can read more about Steam's networking tools [here](https://partner.steamgames.com/doc/api/ISteamNetworkingSockets). Don't let your eyes melt out your head the following HLAPIs all have transports for Steam already built for you just plug and play.

* [FishNetworking](https://github.com/FirstGearGames/FishNet)
* [NetCode ](https://github.com/Unity-Technologies/com.unity.netcode.gameobjects)
* [Mirror](https://github.com/vis2k/Mirror)

Really any HLAPI or Unity Networking package that works with Steamworks.NET (properly) should work out of the box ... see our Installation article for more details.&#x20;

The claims to fame for this one are many and very based on the nature of your game but here are a few key ones we really benefit from in our projects.

* Price Tag = 0.00€ … that's $0.00 or £0.00
* Quality of Service\
  Socks runs over Valve's network so in most cases the round trip is notably faster and less error prone than running over the wild wild web i.e. raw TCP/UDP or KCP based transports. When its not faster ... its just as fast.
* Addresses are CSteamID\
  When used properly your connecting to CSteamIDs not IP/Port so nothing to leak, nothing to fight. This also means no monkeying around with NAT punch or similar.
* Integration\
  As part of the Steam API its trivial to use along side all the rest of Steam's tools and features as described in the Steam API section.

