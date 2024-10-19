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
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Blueprint Nodes

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

See the navigation panel to the left to browse all available nodes.

In Unreal Blueprint editor you can search for nodes by simply typing the node name. In Unreal we have organized the nodes into categories similar to but not limited to the related Steam API interface.

<figure><img src="../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

## Steam ID

You will be working Steam ID a lot, some times you will find it useful either for debugging or player UX to make a human-friendly expression of that ID ... we have tools to help you

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Steam ID to Hex ID simply takes the input Steam ID, finds the unique part of it aka the "Friend" or "Account" ID part of it and we convert that to a hex value such as `ABCD1234` this is a much more human-friendly format than printing a 64bit integral number.

We of course provide the tools to convert back, note that we only hex print the unique part of the Steam ID so you need to tell us what kind of Steam ID it was. To learn more about Steam ID and how it is formed read [our article on the topic here](../../../steam/csteamid.md)!

## Steam Data Types

To simplify node use in Unreal Blueprints we have devolved the Steamworks data types to their respective Blueprint-suitable primitives.&#x20;

### Primitives

* CSteamID --> int64
* AppId\_t --> int32
* AccountId\_t --> int32
* CGameID --> int64

Unreal blueprints do not play nice with unsigned values but Valve expects unsigned values as a result it is up to you to ensure you never pass a value less than zero, the results will be undefined if you do.

In cases where Steam API would work with a char\[] or Linux epoch time we have converted these to the appropriate Blueprint-friendly Unreal-type

### Unreal Types

* Steam int64Time --> FDateTime
* Steam char\* --> FString
