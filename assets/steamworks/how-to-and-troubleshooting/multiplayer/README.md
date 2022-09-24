---
description: Playing with your self is fun, playing with others is even more! ... usually
---

# Multiplayer

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Let’s start by saying this here:

Creating a game is hard work, creating a multiplayer game is extra hard work, creating a massively multiplayer game is … well you get the idea. If this is your first game or even 5th game, I would personally recommend spending some more time creating smaller stand alone projects you can get done from start to finish without complexities like multiplayer. With that out of the way let’s get started.

{% hint style="success" %}
This article covers Steam Multiplayer concepts for more general information on Multiplayer [game design](../../../../company/concepts/design/) please see our [guide on that topic](../../../../company/concepts/design/multiplayer/).&#x20;
{% endhint %}

{% hint style="info" %}
The Networking tool you choose to use does not impact any of the concepts you will learn here.&#x20;

You can use any networking tool you like (NetCode for GameObjects, FIshNetworking, Mirror, etc.), if you want to use the SteamNetworkingSockets interface you should choose a networking tool that has an integration with it.

\
Fish Networking, Mirror and NetCode for GameObjects all have Steam transports that they or their community author. Heathen \*\***does not\*\*** author any of these transports and cannot provide support for them. These transports can be used along side Heathen's Steamworks Complete and Foundation.
{% endhint %}

The [Terminology ](terminology.md)sub section in this article is a must read, with networking concepts especially there are multiple definitions for various terms used and this makes an already confusing topic even more confusing. The terminology section lays out term definitions as we use them here which almost certainty differs from what your used to.

## Preparing your Project

### Step 1

Select the proper Unity Version.

We have a [whole article on this](../../../../company/concepts/fundamentals/unity-release-version.md), long story short you should aim to release your project on the most recent LTS available from Unity.

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

As to general project architecture check out [these articles](../../../../company/concepts/fundamentals/bootstrap-scene.md), concepts such as bootstrap scenes can be a big help in really most projects.

{% hint style="info" %}
Pro Tip

Keep your product project clean and light.



I personally like to set up 2 projects with each "game project" .

1\) The "production" project will be keep clean and I will only ever install just what it needs that is when I import an asset I will exclude its prefabs, samples, documents, etc. keeping only the functional parts I need to use.



2\) The "sandbox" project this is where I pull things in as they where defined by there authors and where I play with my own code and assets making a right mess but designing and iterating quickly



When something is fit for production I simply export it from Sandbox and bring it into Production. This lets me be a messy boy as I design and experiment which I love to do while also keeping the bloat out of the production product.
{% endhint %}
