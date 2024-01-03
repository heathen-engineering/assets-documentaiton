---
cover: ../../../../.gitbook/assets/Unreal Banner@2x.png
coverY: -27.217431192660552
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

# 🔵 Get Launch Query Param

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Gets the associated launch parameter if the game is run via steam://run//?param1=value1;param2=value2;param3=value3 etc.

Parameter names starting with the character '@' are reserved for internal use and will always return an empty string. Parameter names starting with an underscore '\_' are reserved for steam features -- they can be queried by the game, but it is advised that you not param names beginning with an underscore for your own features.

### Key

The launch key to test for for example "param1"

### Return Value

The value associated with the key is provided. Returns an empty string ("") if the specified key does not exist.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>
