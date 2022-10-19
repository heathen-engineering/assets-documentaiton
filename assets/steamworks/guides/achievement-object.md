---
description: Understanding Steam Achievements and the Heathen Engineering tool kit
---

# Achievements

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

{% hint style="info" %}
The above link and repeated below so you can find it:\
[https://partner.steamgames.com/doc/features/achievements](https://partner.steamgames.com/doc/features/achievements)\
\
Is highly important, you should fully read Valve's own documentation around Steam Achievements to fully understand them. Some of the information will be summarized here in and notes on the tools and systems Heathen has created around Steam Achievements is documented below.&#x20;
{% endhint %}

> #### [Valve](https://partner.steamgames.com/doc/features/achievements)
>
> Steam Stats and Achievements provides an easy way for your game to provide persistent, roaming achievement and statistics tracking for your users. The user's data is associated with their Steam account, and each user's achievements and statistics can be formatted and displayed in their Steam Community Profile.

Heathen's Steamworks represents your defined Steam Achievements as scriptable objects associated with the [Steam Settings](../for-unity-game-engine/scriptable-objects/steam-settings/). This allows your unity scripts to reference the achievements as you would any other Unity object e.g. by drag and drop and allows you to perform actions against a given achievement such as to unlock it by calling simple methods on that object.

## What can it do?

Heathen's Steamworks makes working with Steam Achievements as simple as possible.

![](<../../../.gitbook/assets/image (176) (1) (1) (1) (1).png>)

Right from the Steam Settings object you import all of the Steam Achievements you defined in Valve's Steam Developer Portal.

{% hint style="info" %}
You must have the simulation running so the Steam API is initialized and able to talk to Steam client.
{% endhint %}

Once done you can find Scriptable Objects for each of the identified achievements nested under your Steam Settings

![](<../../../.gitbook/assets/image (167) (1) (1) (1) (1) (1) (1) (1) (1).png>)

You can learn more about the [Achievement Object](../for-unity-game-engine/scriptable-objects/achievement-object.md) in our documentation. Using this object you can reference this achievement in any of your own logic and easily test for unlock and unlock the achievement.
