---
description: Making connections
---

# Networking Tools

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Networking tools is a pretty general term and can mean anything from Low Level tools like Steam Networking Sockets, to high level APIs like Fish Networking all the way up to full on platforms such as offered by Photon and Special OS.&#x20;

{% hint style="success" %}
Your an indie not a AAA developer pushing the bleeding edge of what is even possible.

odds are any of these solutions will ( technology wise ) do everything you could dream of plus some so try not to get hung up on "most performant", "MMO SCALE!"?!?!?!", etc. and just look for the tool that suits your project and team. \
\
That will be the tool whose documentation, community and general design "jive" most with you personally.
{% endhint %}

We will list a few commonly used tools in each category below

### Low Level Tools

These are usually low level APIs or frameworks that are meant for use by software engineers looking to implement a particular protocol or networking feature in the engine its self. Unity does have their own Low Level API&#x20;

### High Level Tools

These are often called APIs but are more than just programming tools often including editor extensions and other tools suitable for use by most Unity developers as opposed to being aimed at engineers and programmers.

### Platforms

This is the most diverse set of options, some include Low and High level tools along side backend services and other features. Others go several steps further offering environments for development, testing, etc. in addition to in editor tools. Choosing a platform is less about choosing a technology and more about choosing a networking partner.

## High Level APIs

aka High Level Tools, this is the most common approach for indies to use, its easier than going low level and cheaper than using a full on platform provider. Some examples follow. These are listed in alphabetical order ... we have no favourites.

{% hint style="info" %}
Check out the communities for each of these and find one that suits you. They are all in reality community variants on the old uNET approach and thus they all look and work very similarly.\
\
While we are sure that each developer has put their own spin on the model the differences at a glance are negligible for nearly every use case so find the one whose documentations, community and support suits your needs.
{% endhint %}

### Fish Networking

{% embed url="https://github.com/FirstGearGames/FishNet" %}
Its out of beta now but the GitHub site hasn't updated its name
{% endembed %}

### Mirage

{% embed url="https://github.com/MirageNet/Mirage" %}

### Mirror

{% embed url="https://github.com/vis2k/Mirror" %}

### Net Code for GameObjects aka MLAPI

{% embed url="https://docs-multiplayer.unity3d.com/" %}

### Net Code for Entities (sorta DOTS)

{% embed url="https://github.com/Unity-Technologies/multiplayer" %}

### Riptide

{% embed url="https://github.com/tom-weiland/RiptideNetworking" %}

## Platforms

These are far less commonly used by indies but offer some interesting usually very niche options.

### Photon

{% embed url="https://www.photonengine.com/" %}

### Reactor

{% embed url="https://www.kinematicsoup.com/" %}

### SpacialOS

{% embed url="https://ims.improbable.io/products/spatialos" %}

## Low Level APIs

Typically an indie would select an HLAPI (High Level API) and then choose from the "transports" it supports. You could however forgo using a HLAPI and integrate the low level framework, protocol, etc. directly.

TCP, UDP, etc. are all obvious options but really if your going that way why not use an existing plugin. The options below again have transports available in most HLAPIs but worth mention here.

### Game Networking Sockets

{% embed url="https://github.com/ValveSoftware/GameNetworkingSockets" %}

### KCP

{% embed url="https://github.com/skywind3000/kcp" %}
