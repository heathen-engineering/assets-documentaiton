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

# 🔵 Set Game Tags

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
Only valid for Steam Game Servers
{% endhint %}

Sets a string defining the "gametags" for this server, this is optional, but if set it allows users to filter in the matchmaking/server-browser interfaces based on the value.

This is usually formatted as a comma or semicolon separated list.

Don't set this unless it actually changes, its only uploaded to the master once; when acknowledged.

### Data

The new "gametags" value to set. Must not be **NULL** or an empty string (""). This can not be longer than 128

## Nodes

<figure><img src="../../../../.gitbook/assets/image (288).png" alt=""><figcaption></figcaption></figure>
