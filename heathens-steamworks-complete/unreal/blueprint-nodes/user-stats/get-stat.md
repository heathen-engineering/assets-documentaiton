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

# 🔵 Get Stat

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Several options are available for reading a stat value for the local user, a specific user, for the user's value, the global value of the stat or the historical value of an averaged stat.

### API Name

The name of the achievement to get

### Return Value

A [Float Stat](../types/float-stat.md) or [Int Stat](../types/int-stat.md) value indicates rather or not the process was valid (API name found and read) and what the value read was.

Global stats return the value as a float or int directly, history stats return via a callback event an array containing the values and a [UEResult](../enumerators/ueresult.md) indicating the status of the request.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (326).png" alt=""><figcaption></figcaption></figure>
