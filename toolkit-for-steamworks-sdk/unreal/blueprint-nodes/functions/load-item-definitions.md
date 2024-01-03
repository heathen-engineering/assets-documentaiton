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

# 🔵 Load Item Definitions

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Triggers an asynchronous load and refresh of item definitions.

Item definitions are a mapping of "definition IDs" (integers between 1 and 999999999) to a set of string properties. Some of these properties are required to display items on the Steam community website. Other properties can be defined by applications. There is no reason to call this function if your game hardcoded the numeric definition IDs (e.g. purple face mask = 20, blue weapon mod = 55) and does not allow for adding new item types without a client patch.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (746).png" alt=""><figcaption></figcaption></figure>
