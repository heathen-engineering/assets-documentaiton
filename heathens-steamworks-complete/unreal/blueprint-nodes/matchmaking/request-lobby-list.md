---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
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

# 🔵 Request Lobby List

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

To get a list of lobbies such as to populate a lobby browser, or far more commonly to simply take the first lobby returned and join it. You must first define your lobby filter, see the [Add Request Lobby List Filter](add-request-lobby-list-filter.md) article for more information on that process.&#x20;

When the filter has been established call Request Lobby List, this will have a single input called `Callback` which is an event that will report the count of lobbies found. You can then loop over that count and using Get Lobby by Index you can return the ID of each lobby returned.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>
