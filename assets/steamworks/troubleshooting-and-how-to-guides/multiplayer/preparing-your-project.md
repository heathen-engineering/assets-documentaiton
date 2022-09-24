---
description: On your mark, Get set .... CODE
---

# Preparing your Project

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The following sections break down the major things to get done and in order before you do anything else.

## Update Unity

Select the proper Unity Version.

We have a [whole article on this](../../../../company/concepts/fundamentals/unity-release-version.md), long story short you should aim to release your project on the most recent LTS available from Unity.

## Prerequisites

Installing requirements

Pick a HLAPI you like and go with it, I will use NetCode for GameObjects in the rest of this not because its best or my favourite, etc. but because it’s the "standard" Unity pushes.

For all there hemming and hawing about how there HLAPI is the best-ist ever, most are so strikingly similar that if you’re bumping up against the differences in a way that hurts your game you might want to consider a custom solution more specific to your game … its easier than you might think. We might cover that in a later topic.

Aside from your HLAPI of choice you will need of course

Steamworks.NET

Heathen’s Steamworks (I suggest Complete, but Foundation might do you)

[UX Complete](../../../ux/) can be a big help as well if you want to [manager your scenes directly](../../../ux/components/scenes-manager.md) though some HLAPI NMs do some crude scene management.

## Configuring Steam

Setting up your Steam project. If your going with a P2P model nothing special to be done here but if your going with a Client Server set up and intend to build a [Steam Game Server](game-server-browser.md) you then you also need to configure your Steam App for that. You can read more in Valve's own documentation for Steam Game Server [here](https://partner.steamgames.com/doc/features/multiplayer/game\_servers).

For general understanding of what [P2P ](../../../../company/concepts/design/multiplayer/#peer-to-peer-p2p)vs[ Client/Server](../../../../company/concepts/design/multiplayer/#client-server) is please read our [design article](../../../../company/concepts/design/multiplayer/). Interestingly a lot of people have a miss conception as to what P2P and Client/Server mean ... its wise to click those links and check the terminology.

As to general project architecture check out [these articles](../../../../company/concepts/fundamentals/bootstrap-scene.md), concepts such as bootstrap scenes can be a big help in really most projects.

{% hint style="info" %}
Pro Tip

Keep your product project clean and light.



I personally like to set up 2 projects with each "game project" .

1\) The "production" project will be keep clean and I will only ever install just what it needs that is when I import an asset I will exclude its prefabs, samples, documents, etc. keeping only the functional parts I need to use.



2\) The "sandbox" project this is where I pull things in as they where defined by there authors and where I play with my own code and assets making a right mess but designing and iterating quickly



When something is fit for production I simply export it from Sandbox and bring it into Production. This lets me be a messy boy as I design and experiment which I love to do while also keeping the bloat out of the production product.
{% endhint %}
