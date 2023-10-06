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

# 🔵 Serialize Result

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Gets the state of a subset of the current user's inventory.\
\
The subset is specified by an array of item instance IDs.\
\
The results from this call can be serialized using the Serialize Result node and passed to other players to "prove" that the current user owns specific items, without exposing the user's entire inventory. For example, you could call this with the IDs of the user's currently equipped items serialize this to a buffer, and then transmit this buffer to other players upon joining a game.

### Instance Ids

The array of instance IDs to serialize

### Return Value

An Inventory Result object defining the handle and success state.

### Example

This process requires two steps, first request a result handle with the desired items

<figure><img src="../../../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

The second part is to listen on the Steam Inventory Result Ready event callback and when received check it against your expected handle, if it is the handle for your request Serialize Result produces an array of bytes that can be sent over the network and destroy the handle.

<figure><img src="../../../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>
