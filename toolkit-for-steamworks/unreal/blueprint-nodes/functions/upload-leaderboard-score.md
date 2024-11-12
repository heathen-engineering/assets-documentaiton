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

# 🔵 Upload Leaderboard Score

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Uploads a score and data to a leaderboard for the current user

### Board ID

The ID of the board to upload to

### Keep Best

Should the board only keep the upload if the value is better than the existing value

### Data

An array with a max length of 64 of ints that can be used to store additional data on the board

### Return Value

A callback event that indicates success, score changed, the new rank if any and the old rank if any

## Nodes

<figure><img src="../../../../.gitbook/assets/image (329).png" alt=""><figcaption></figcaption></figure>
