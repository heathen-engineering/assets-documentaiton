---
description: Setting up and using Steam Input in your game
---

# 🖱 Input

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Input allows you to define "actions" for your game which can be mapped and bound by the Steam client (outside your game) enabling any controller the player may have to simply work.

In practice, Steam Input is very much like Unity's "new" Input System and 3rd party Unity assets such as Rewired. Steam Input is not a requirement to publish your game on Steam or to achieve Steam Deck verification.

Steam Input cannot be used for Keyboard and Mouse bindings in that it was designed specifically for use with controllers that are being mapped by Steam client.

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/features/steam\_controller](https://partner.steamgames.com/doc/features/steam\_controller)
* In-Game Action File Documentation\
  [https://partner.steamgames.com/doc/features/steam\_controller/iga\_file](https://partner.steamgames.com/doc/features/steam\_controller/iga\_file)

</details>

## Quick Start

First you will need to define the actions your game has, this is done via an In-Game Action file which is a JSON-style file located at the root of the project. See [https://partner.steamgames.com/doc/features/steam\_controller/iga\_file](https://partner.steamgames.com/doc/features/steam\_controller/iga\_file) for more information.

## In-Game Action file

This is how you define what action sets, layers and actions your game has and how they are used (loosely). Using this Steam's controller binding system can be used to map various controls to your actions and your game can thus be blissfully unaware of what IO device is driving the game.
