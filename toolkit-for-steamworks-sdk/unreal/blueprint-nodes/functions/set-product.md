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

# 🔵 Set Product

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

Sets the game product identifier. This is currently used by the master server for version-checking purposes.

Converting the game's app ID to a string for this is recommended.

{% hint style="info" %}
This is required for all game servers and can only be set before calling [Log On](log-on.md) / [Log On Anonymous](log-on-anonymous.md)
{% endhint %}

### Product

The unique identifier for your game. Must not be **NULL** or an empty string. Sets the game product identifier. This is currently used by the master server for version-checking purposes.

Converting the game's app ID to a string for this is recommended.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (809).png" alt=""><figcaption></figcaption></figure>
