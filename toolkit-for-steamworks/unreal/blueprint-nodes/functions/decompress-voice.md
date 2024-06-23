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

# 🔵 Decompress Voice

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Decodes the compressed voice data returned by [Get Voice](get-voice.md).\
\
The output data is raw single-channel 16-bit PCM audio. The decoder supports any sample rate from 11025 to 48000. See [Get Voice Optimal Sample Rate](get-voice-optimal-sample-rate.md) for more information.

### Compressed Data

The array of bytes that represents the compressed data

### Desired Sample Rate

The sample rate that will be returned. This can be from **11025** to **48000**, you should either use the rate that works best for your audio playback system, which likely takes the user's audio hardware into account, or you can use [Get Voice Optimal Sample Rate](get-voice-optimal-sample-rate.md) to get the native sample rate of the Steam voice decoder.

### Return Value

A [Decompress Voice Result](../types/decompress-voice-result.md) value containing the results and data of the process

## Nodes

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
