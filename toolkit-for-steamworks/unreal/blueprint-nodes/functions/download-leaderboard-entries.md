---
cover: ../../../../.gitbook/assets/Unreal Banner.jpg
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

# 🔵 Download Leaderboard Entries

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Fetches a series of leaderboard entries for a specified leaderboard. You can ask for more entries than exist, then this will return as many as do exist.

### Board ID

The board to read from

### Request Type

The [UELeaderboardDataRequest](../enumerators/ueleaderboarddatarequest.md) type to request from the board.

### Start

The index to start downloading entries relative to eLeaderboardDataRequest.

### End

The last index to retrieve entries for relative to eLeaderboardDataRequest.

### Detail Count

The number of detail entries to read from the entry

### Callback

An event that will be called when complete and contains an array of [Leaderboard Entry](../types/leaderboard-entry.md)

## Nodes

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
