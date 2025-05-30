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

# 🔵 Get Available Voice

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Checks to see if there is captured audio data available from [Get Voice](get-voice.md), and gets the size of the data.\
\
Most applications will only use compressed data and should ignore the other parameters, which exist primarily for backwards compatibility. See [Get Voice](get-voice.md) for further explanation of "uncompressed" data.

### Return Value

A [Voice Available Result](../types/voice-available-result.md) object expressing the state of the system and the amount of data available to be read

## Nodes

<figure><img src="../../../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>
