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

# BP\_SteamAvatarImage

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

An extension of the standard UImage widget with two new functions to help display a Steam Avatar image for the local player or a specified user.

## Functions

### Show My Avatar

<div align="left">

<figure><img src="../../../.gitbook/assets/image (13) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

This works with the[ Get My Steam Avatar](../blueprint-nodes/functions/get-my-steam-avatar.md) method to handle loading the local user's avatar image for you and assigning it to the Image for display.

### Show User Avatar

<div align="left">

<figure><img src="../../../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

</div>

This works with the [Get User Steam Avatar](../blueprint-nodes/functions/get-user-steam-avatar.md) method to handle loading a target user's avatar image for you and assigning it to the image for the display.

## Example

<figure><img src="../../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

The process assumes you have added a BP\_SteamAvatarImage to your UI. We then get the Steam Avatar Image from your UI and use that as the target input for the Show My Avatar function call.

To set the avatar for another user the process is the same with the addition of needing to get the desired user's ID. There are many places where you might get a user's ID and want to display their avatar such as the members of a lobby you are in, your friend list, the users on a server, the entries in a leaderboard or even the other player's on a Steam Game Server.
