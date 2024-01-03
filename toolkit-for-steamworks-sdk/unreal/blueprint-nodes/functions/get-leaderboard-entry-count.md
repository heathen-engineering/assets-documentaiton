---
cover: ../../../../.gitbook/assets/Unreal Banner@2x.png
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

# 🔵 Get Leaderboard Entry Count

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Returns the total number of entries in a leaderboard.\
\
This is cached on a per-leaderboard basis upon the first call to [Find Leaderboard](find-leaderboard.md) or [Find Or Create Leaderboard](find-or-create-leaderboard.md) and is refreshed on each successful call to [Download Leaderboard Entries](download-leaderboard-entries.md), [Download Leaderboard Entries for Users](download-leaderboard-entries-for-users.md), and [Upload Leaderboard Score](upload-leaderboard-score.md).

### Board ID

The ID of the board

### Return Value

The number of entries on the board

## Nodes

<figure><img src="../../../../.gitbook/assets/image (848).png" alt=""><figcaption></figcaption></figure>
