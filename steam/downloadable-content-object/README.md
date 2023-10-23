---
description: Understanding Steam DLC and the Heathen Engineering tool kit
---

# 🕹 Downloadable Content

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Downloadable Content aka DLC allows you to sell expansions, seasons and other add-ons for your game through the Steam store and reliably and securely detect when a user owns that add-on

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/store/application/dlc](https://partner.steamgames.com/doc/store/application/dlc)

</details>

## Quick Start

First, you need to create your DLC on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

### Create

Log into your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

From there scroll down until you find the All DLC section and click Add New DLC button

<figure><img src="../../.gitbook/assets/image (5) (1) (4).png" alt=""><figcaption></figcaption></figure>

Populate the form with the names of the DLC you would like to create making sure to start the name with the name of your game. For example, our game's name is Túatha Legends so we might a DLC something like Túatha Legends - The Iron King

### Publish

You \*\***MUST**\*\* publish your changes in the Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>
