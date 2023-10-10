---
description: On your mark, Get set .... CODE
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

<details>

<summary>Unity</summary>

### Update Unity

Select the proper Unity Version, this is much more important than you might think. You should be keeping your Unity Editor up to date with what you anticipate will be the most recent 'LTS' build of Unity at the time your game launches. We have a [whole article on this](../../../fundamentals/unity-release-version.md), it explains what LTS is, why we have this stance and how to go about it.

### Installing Requirements

You have options in how you deliver a multiplayer experience for your players.&#x20;

#### Local Multiplayer

Local multiplayer is the simplest and least common in the current market, especially for PC games. This method doesn't require any additional technology beyond a means to understand when input comes from 1 player vs. the others. Steam Input identifies each controller uniquely so this is a trivial matter usually accomplished by asking each player to press a button to "register" and then associating that controller with that player.

#### Remote Play

This is a feature of&#x20;

## Networking

Installing requirements

Pick an HLAPI you like and go with it, I will use NetCode for GameObjects in the rest of this not because it's best or my favourite, etc. but because it’s the "standard" Unity pushes.

For all their hemming and hawing about how their HLAPI is the best, most are so strikingly similar that if you’re bumping up against the differences in a way that hurts your game you might want to consider a custom solution more specific to your game … its easier than you might think. We might cover that in a later topic.

Aside from your HLAPI of choice, you will need of course

Steamworks.NET

Heathen’s Steamworks (I suggest Complete, but Foundation might do you)

[UX Complete](../../../../assets/ux/) can be a big help as well if you want to manage[ your scenes directly](../../../../assets/ux/components/scenes-manager.md) though some HLAPI NMs do some crude scene management.

## Configuring Steam

Setting up your Steam project. If you going with a P2P model nothing special to be done here but if you're going with a Client-Server setup and intend to build a [Steam Game Server](game-server-browser/) then you also need to configure your Steam App for that. You can read more in Valve's documentation for Steam Game Server [here](https://partner.steamgames.com/doc/features/multiplayer/game\_servers).

For a general understanding of what [P2P ](../../../design/multiplayer/#peer-to-peer-p2p)vs[ Client/Server](../../../design/multiplayer/#client-server) is please read our [design article](../../../design/multiplayer/). Interestingly a lot of people have a misconception as to what P2P and Client/Server mean ... its wise to click those links and check the terminology.

As to general project architecture check out [these articles](../../../design/bootstrap-scene.md), concepts such as bootstrap scenes can be a big help in most projects.

</details>

<details>

<summary>Unreal</summary>

Unreal's approach to multiplayer is significantly more mature and able. Simply install the [Steam Sockets plugin](https://docs.unrealengine.com/5.3/en-US/using-steam-sockets-in-unreal-engine/) to enable the Steam Sockets netdriver.&#x20;

Note that you do not need to use Online Subsystem Steam if you are using Heathen's Steamworks Complete.

[Online Subsystem Steam](https://docs.unrealengine.com/5.3/en-US/online-subsystem-steam-interface-in-unreal-engine/) is a bare-bones Steamworks SDK integration written by Epic directly. It lacks full support for all of Steam APIs features but provides the basics. [Heathen's Steamworks Compelte](../../../../heathens-steamworks-complete/unreal/) on the other hand is a full-featured integration and toolkit expanding on Steam API and integrated deeply with the engine.

</details>

