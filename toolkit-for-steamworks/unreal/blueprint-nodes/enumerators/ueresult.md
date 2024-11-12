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

# 🟨 UEResult

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Steam error result codes.

These are frequently returned by functions, callbacks, and call results from both the Steamworks API and the Web API. An API may return arbitrary EResult codes, refer to the documentation for that API function or callback to see what it could return and what they mean in the context of that API call. This is similar to Win32's HRESULT type or POSIXs errno.

Heathen's UEResult is a blueprint-friendly wrapper around this common enum

{% embed url="https://partner.steamgames.com/doc/api/steam_api#EResult" %}

## Nodes

<figure><img src="../../../../.gitbook/assets/image (18) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
