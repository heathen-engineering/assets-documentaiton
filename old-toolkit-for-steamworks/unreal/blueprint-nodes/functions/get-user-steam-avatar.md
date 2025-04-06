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

# 🔵 Get User Steam Avatar

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Loads the target user's Steam Avatar image into a Unreal Texture 2D and invokes an event when completed.

### Id (Input)

The user you want to get the avatar for

## Nodes

<figure><img src="../../../../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

This node uses a callback delegate which will be invoked when the process is completed and which will contain the Texsture2D result.
