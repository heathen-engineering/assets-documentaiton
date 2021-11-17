---
description: Understanding Steam Leaderboards and the Heathen Engineering tool kit
---

# Leaderboards

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

Steam leaderboards are persistent tables with automatically ordered entries. Leaderboards can be used to display global and friend boards in your game and on your community page. Each title can create up to 10,000 leaderboards, and each leaderboard can be retrieved immediately after a player's score has been uploaded.

There is no limit on the number of players a leaderboard supports. Each leaderbaord entry contains a score (as an int) and optionally up to 64 ints of detail data stored as a simple array on the entry. The detail data can be used to store game specific information about the play session that resulted in the user's leaderboard entry. This data is not sorted or parsed by Steam, and is replaced when a new leaderboard entry is created for the user. Attachments can be linked with the leaderboard via the UGC (User Generated Content) feature of Steam.

Leaderboards can be configured such that only a trusted web API call can set the value. This is strongly recommended if you have any concern over the validity of leaderboard scores. When the leaderboard's write operation is configured as trusted only a server using the Steam Web API and a publisher token can upload scores to the board. If the board is not configured as trusted write then anyone can upload any score to the board.

{% hint style="info" %}
Use the Steam Web API to set trusted leaderboard scores

[https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore](https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore)
{% endhint %}

## Leaderboard Object

This is a scriptable object used to define the leaderboard in Unity and used within Unity to query the board and access its information. Read more in the [Leaderboard Object](../objects/leaderboard.md) document.

### To Create

To create a Leaderboard Object press the "<mark style="color:green;">+ New</mark>" button on the Steam Settings object next to the Leaderboards entry

{% hint style="info" %}
Unfortunately we cannot import existing leaderboards from Steam directly.



Why?

Valve have not provided an official means to do so through the Steam API.
{% endhint %}

![](<../../../.gitbook/assets/image (182).png>)
