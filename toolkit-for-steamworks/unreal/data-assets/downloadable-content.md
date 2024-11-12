---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Downloadable Content

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Steam DLC (Downloadable Content) is one of the best and least problematic methods for extending the revenue potential of your game.&#x20;

Contrary to their name they do not -**have-** to contain content that is downloaded, a more appropriate name for them would be Child App IDs ... that is what they are technically speaking but that isn't a very marketable name.

A DLC is just an App ID, it is a child of your main app, you can use it to understand what extras your user owns and where each user can purchase and thus own each of these no more than 1 time ... e.g. they are not MTX consumables. These can thus represent expansions, unlocks, skin packs, collectors editions, bonus packs or indeed, literal downloadable content related to your game such as soundtracks, guides and more.

You would define the DLC your main app has in the Steamworks Developer Portal and can then represent your DLC in your game content via a Downloadable Content Data Asset.

## Create

Create a new Data Asset Instance of type DownloadableContentDataAsset

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## Configure

Set the Application ID assigned to the DLC in Steamworks Developer Portal

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## Use

To use the DLC you can simply create a variable of type DownloadableContentDataAsset and set its default value to be the instance you just created.

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

With the variable set you can simply drag off that variable to access the functions and features of a Steam DLC relative to this specific DLC.

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
