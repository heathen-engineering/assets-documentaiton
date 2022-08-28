---
description: Sadly abused in every way
---

# 😡 Non-Fungible Tokens (NFTs)

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="danger" %}
Predatory in every known use case (see [Play to Earn](../../models/play-to-earn.md))&#x20;
{% endhint %}

{% embed url="https://www.youtube.com/watch?t=216s&v=GzTj60CWhQo" %}
Video in Portuguese&#x20;
{% endembed %}

{% embed url="https://docs.google.com/presentation/d/1a8dMxaqyjWl4G6NO7mXF30CICHOJLkJxuP2Xrpky9rA/edit#slide=id.g1368c24f233_0_57" %}
English Translated Slides
{% endembed %}

Everyone loves to hate NFTs in games at the moment and its important to understand that and understand why.

## What is a NFT

Non-Fungible Token ... dumb choice of wording to mean a serialized ID e.g. a unique ID.

To understand in detail we need dedicated articles so look [here ](blockchain-and-nfts.md)for more. In short though its simply a unique identifiable record in a distributed database. It really amounts to not a lot more than a unique identifier associated with some transactions and maybe some metadata depending on the chain and implementation in question.

## How are NFTs used

NFTs can be used in relation to games in a lot of different ways and some of those ways have nothing to do with monetization. When they are monetization based the NFT is no different than DLC licenses or more frequently simply as digital Items.

{% hint style="info" %}
Sadly NFTs in games are most commonly used for [Play to Earn monetization models](../../models/play-to-earn.md) which are highly predatory and problematic for the user, the industry and in many cases the companies that try it.
{% endhint %}

### NFT Licenses

{% hint style="success" %}
In Heathen's humble personal opinion this is at current the best use case for NFTs in game.\
\
But still doesn't make practical since with other technologies being vastly superior to Blockchain options.
{% endhint %}

Put simply this is using NFTs to track ownership of the license of the game, DLC or other licensable content. This is most similar to the concepts you see touted for artists, the massive difference here being a game and its backend systems can make them selves dependent on a valid token where as an offline bit of art or even digital art has no programmatic way to validate.

This use would see your game require the user to "authenticate" ownership by proving ownership of a NFT representing the license to the game. This of course still requires a backend service to perform that validation and grant access to the live services backing the game. If the game was wholly offline circumventing this would be as trivial as CD Keys where in the past.

That said if your game has a backend service then that backend service already has an account authentication solution and likely already has the ability to transfer ownership of license between accounts. So even this use case doesn't really offer anything that isn't already available. This use for NFTs would mean that players could trade and resale games even outside the developers platform however the need to authenticate means that some platform must still act as a centralized authority defeating the purpose of NFT at all.

{% hint style="info" %}
Now if your looking to create a backend service; then using blockchain technology internally might be of interest in that it is an interesting way to track and prove validity of transactions. Its not the only way and I question rather its the best way but it is "a" way that may be worth looking into.
{% endhint %}

### NFT Items

Very similar to NFT Licenses really, the idea is in-game digital items are represented as an NFT as a result ownership is determined by possession of the NFT. However this still requires a backend service to validate and authenticate. Such services already have the means to enable community marketplaces so there is no benefit here at all.

You could argue that NFTs allow the user to perform transactions outside the control of the developer. I would then point out that so can Steam Inventory and many other systems. The main benefit here is that NFTs are not really platform dependent in and of them selves so that license of ownership could exist beyond the platforms life. The obvious "who cares" with that is the platform is the content, the NFT is just the license a license to nothing is still nothing.

{% hint style="info" %}
As with the above NFT Licensing, if you where a platform provider, using blockchain technology might be interesting in that it could allow transactions outside your platform to still be valid and secure ... theoretically. \
\
Blockchain and NFT isn't the only way to do that and I again would question if its the best way to do that but it would be an interesting topic to look into. Also by allowing transactions out side of your control cons and other exploits run rampant ... just google NFT theft or scam and read any entry you like.
{% endhint %}

### Other concepts

Smart contracts and other features of Blockchain technology are present but not of much value at current. Ideas such as driving player issued quests, tracking item history and using that to evolve an item over multi-user life are all very interesting to think about. None of them are however dependent on Blockchain technology and to date we have not yet found a use case where Blockchain was the better solution to such a problem.

{% hint style="info" %}
Its worth noting that Heathen as a company is exploring Blockchain as a technology as we do with every technology we can research.\
\
We do create integrations between Blockchain web APIs and Unity and are exploring game systems such as inventory, crafting, questing and others driven by Blockchain. We believe there may be potential in the technology is just not quit there yet. Every use case at current can be had with better value through other means.

\
Heathen is defiantly not a "NFT Bros." but we are also not a "Hater" of Blockchain or NFT for the sake of it.&#x20;
{% endhint %}
