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

# BP\_SteamUserName

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

An extension of the standard UTextBlock widget with three new functions to help display a Steam name or nickname for the local player or a specified user.

## Functions

### Show My Name

![](<../../../.gitbook/assets/image (207).png>)

This works with the Get Persona Name method to handle loading a target user's name for you and assigning it to the display.

### Show User Name

![](<../../../.gitbook/assets/image (208).png>)

This works with the Get Friend Persona Name method to handle loading a target user's name for you and assigning it to the display.

### Show User Nickname

![](<../../../.gitbook/assets/image (209).png>)

This works with the Get Player Nickname method to handle loading a target user's name for you and assigning it to the display.

{% hint style="info" %}
A Nickname is a name that the local user has assigned to another user.

In short Name = what the user calls themselves whereas Nickname = what the local user calls this user.

\
A real-world example would be if you were friends with a brother named Jack. Jack may set his Steam name to 4pple54ouce ... but you can of course set the Nickname to Jack. For you in your friends list you see Jack ... everyone else (who hasn't set a nickname for him) will see 4pple54ouce.

\
Given this, there is no such thing as a Nickname for the local user. The local user calls themselves what they have assigned to Name.
{% endhint %}

## Example

<figure><img src="../../../.gitbook/assets/image (206).png" alt=""><figcaption></figcaption></figure>

The process assumes you have added a BP\_SteamUserName to your UI. We then get the Steam Name from your UI and use that as the target input for the Show My Name function call.

To set the name for another user the process is the same with the addition of needing to get the desired user's ID. There are many places where you might get a user's ID and want to display their avatar such as the members of a lobby you are in, your friend list, the users on a server, the entries in a leaderboard or even the other player's on a Steam Game Server.
