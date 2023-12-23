---
description: Getting started with Steam Multiplayer
---

# ☝ Getting Started

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

So you want to build a multiplayer Steam game? We can help!

Your first stop should be our [Design article on Multiplayer](../../../design/multiplayer/) it covers the fundamentals that you'll need to know before you get started. Once you have your head wrapped around the concepts and a design in mind come back here and we will get started.

### Local Multiplayer

Local multiplayer is the simplest and least common in the current market, especially for PC games. This method doesn't require any additional technology beyond a means to understand when input comes from 1 player vs. the others. Steam Input identifies each controller uniquely so this is a trivial matter usually accomplished by asking each player to press a button to "register" and then associating that controller with that player.

### Remote Play

This is a feature of Steam API where a remote player can Steam into your local game. Your game will see this user as another local user so if your game is configured for local multiplayer this can usually be used right out of the box

## Unity

### Networking

Installing requirements

Pick an HLAPI you like and go with it, I will use NetCode for GameObjects in the rest of this not because it's best or my favourite, etc. but because it’s the "standard" Unity pushes.

For all their hemming and hawing about how their HLAPI is the best, most are so strikingly similar that if you’re bumping up against the differences in a way that hurts your game you might want to consider a custom solution more specific to your game … its easier than you might think. We might cover that in a later topic.

Aside from your HLAPI of choice, you will need of course

Steamworks.NET

Heathen’s Steamworks (I suggest Complete, but Foundation might do you)

[UX Complete](../../../../assets/ux/) can be a big help as well if you want to manage[ your scenes directly](../../../../assets/ux/components/scenes-manager.md) though some HLAPI NMs do some crude scene management.

### Configuring Steam

Setting up your Steam project. If you going with a P2P model nothing special to be done here but if you're going with a Client-Server setup and intend to build a [Steam Game Server](game-server-browser/) then you also need to configure your Steam App for that. You can read more in Valve's documentation for Steam Game Server [here](https://partner.steamgames.com/doc/features/multiplayer/game\_servers).

For a general understanding of what [P2P ](../../../design/multiplayer/#peer-to-peer-p2p)vs[ Client/Server](../../../design/multiplayer/#client-server) is please read our [design article](../../../design/multiplayer/). Interestingly a lot of people have a misconception as to what P2P and Client/Server mean ... its wise to click those links and check the terminology.

As to general project architecture check out [these articles](../../../design/bootstrap-scene.md), concepts such as bootstrap scenes can be a big help in most projects.

## Unreal

Unreal's built-in networking tools and features are unaffected by Steam API and will work as normal. The only consideration to keep in mind is regarding the Online Subsystem. The following link explains what an Online Subsystem is and how it relates to Steamworks Complete.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/online-subsystem.md" %}
[online-subsystem.md](../../../../toolkit-for-steamworks-sdk/unreal/online-subsystem.md)
{% endcontent-ref %}

The Net Driver you choose defines how you will connect, Unreal's built-in Steam Sockets Net Driver is unfortunately out of date and dependent on the incompatible Online Subsystem Steam.&#x20;

{% hint style="info" %}
Heathen has created a Steam Networking Sockets Net Driver that is compatible with Heahten's Steamworks Complete and is not dependent on an Online Subsystem.\
\
The Net Driver is in preview and currently only available to [GitHub Sponsors](../../../../become-a-sponsor/). Once the driver has been tested and proven it will be added to the Steamworks Complete plugin.
{% endhint %}
