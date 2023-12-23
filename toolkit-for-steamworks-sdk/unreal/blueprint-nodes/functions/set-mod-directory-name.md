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

# 🔵 Set Mod Directory Name

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

Sets the game directory.

This should be the same directory where the game gets installed into. Just the folder name, not the whole path. e.g. "Spacewar".

{% hint style="info" %}
This is required for all game servers and can only be set before calling [Log On](log-on.md) / [Log On Anonymous](log-on-anonymous.md)
{% endhint %}

### Directory Name

The game directory to set. Must not be **NULL** or an empty string (""). This can not be longer than 32

## Nodes

<figure><img src="../../../../.gitbook/assets/image (291).png" alt=""><figcaption></figcaption></figure>
