---
description: Making connections
---

# Networking Tools

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what you are seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Networking tools is a pretty general term and can mean anything from Low-Level tools like Steam Networking Sockets to high-level APIs like Fish Networking up to full-on platforms such as those offered by PlayFab, GameLift, etc.&#x20;

{% hint style="success" %}
You are an indie, not a AAA developer pushing the bleeding edge of what is even possible.

odds are any of these solutions will (technology-wise) do everything you could dream of plus some. Try not to get hung up on "most performant", or "MMO SCALE!"?!?!?!", etc. and just look for the tool that suits your project and team. \
\
That will be the tool whose documentation, community and general design "jive" most with you personally, your project and with the rest of your team.
{% endhint %}

We will list a few commonly used tools in each category below

### Unity

Unity doesn't have a pre-defined or standardized approach to multiplayer. On one hand, this means you have more flexibility and can generally do what you feel works best. On the other hand, it means you have to sort out how you will do everything, from syncing data to game objects, serializing data for transmission, etc. Unity has loads of tools and plug-ins to help with various aspects, the most common of which being "HLAPI"s or High-Level Application Interfaces: A few common examples follow

{% hint style="info" %}
[Heathen's Toolkit for Steamworks](../../../toolkit-for-steamworks-sdk/steamworks.md) is available for Unity, Unreal and Godot and integrates the full feature set of Steamworks / Steam API with your game.\
\
No matter what HLAPI you choose if you want to work with Steam Networking Sockets you will need to integrate Steamworks SDK / Steam API with your game.
{% endhint %}

#### Fish Networking

{% embed url="https://github.com/FirstGearGames/FishNet" %}
Its out of beta now but the GitHub site hasn't updated its name
{% endembed %}

#### Mirage

{% embed url="https://github.com/MirageNet/Mirage" %}

#### Mirror

{% embed url="https://github.com/vis2k/Mirror" %}

#### Net Code for GameObjects aka MLAPI

{% embed url="https://docs-multiplayer.unity3d.com/" %}

#### Net Code for Entities (sorta DOTS)

{% embed url="https://github.com/Unity-Technologies/multiplayer" %}

#### Riptide

{% embed url="https://github.com/tom-weiland/RiptideNetworking" %}

### Unreal

Unreal is built with networking in mind fundamentally. That is networking is simply part of the engine and doesn't (strictly speaking) require any additional plugins or tools. Unreal does offer additional plugins to expand its capabilities such as "Online Subsystems" that integrate with various services such as Google, Facebook, etc in a standardized way.

Online Subsystems have a notable drawback when working with Steam or other rich featured platforms in that the Online Subsystem approach seeks to "normalize" the feature set to the commonly available features.

{% hint style="info" %}
[Heathen's Toolkit for Steamworks](../../../toolkit-for-steamworks-sdk/steamworks.md) is available for both Unreal and Unity and integrates the full feature set of Steamworks / Steam API with your game&#x20;
{% endhint %}

## Platforms

These are far less commonly used by indies but offer some interesting options.

### GameLift

A full LiveOps service based on Amazon Web Services (AWS). Together with PlayFab these are the most service and feature-complete options available.&#x20;

{% embed url="https://aws.amazon.com/gamelift/" %}

### G-Portal

A popular solution for Survival games and other genres where dedicated servers hosted by players or your selves (private and official servers) are needed but with less overhead and complexity than a full LiveOps service or a hybrid service like Photon.

{% embed url="https://www.g-portal.com/en" %}

### Photon

An early entry into the market, initially a solution for easily accessible Multiplayer services available for Unity and Unreal.

{% embed url="https://www.photonengine.com/" %}

### PlayFab

A full LiveOps service based on Microsoft's Azure. Together with GameLift these are the most service and feature-complete options available.&#x20;

{% embed url="https://playfab.com/" %}

### Reactor

{% embed url="https://www.kinematicsoup.com/" %}
