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

# 🔵 Find or Create Leaderboard

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Gets a leaderboard by name. The resulting ID will be valid for the duration of the game session, you should in general cash this value early and use it for future operations against the board.

### API Name

The name of the board to find or create

### Sort Method

How should the board be sorted

* Ascending\
  The top-rank is the lowest score value.
* Descending\
  The top-rank is the highest score value.

### Display Type

The display type used by the Steam Community website to know how to format the leaderboard scores when displayed.

* Numeric\
  The score is just a simple numerical value.
* Time Seconds\
  The score represents a time, in seconds.
* Time Milliseconds\
  The score represents a time, in milliseconds.

### Callback

An event that will be called when complete and contains the board ID.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
