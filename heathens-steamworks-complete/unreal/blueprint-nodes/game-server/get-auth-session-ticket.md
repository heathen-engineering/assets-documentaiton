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

# 🔵 Get Auth Session Ticket

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

Retrieve an authentication ticket to be sent to the entity that wishes to authenticate you.\
\
After calling this you can send the ticket to the entity where they can then call Begin Auth Session to verify this entity's integrity.

### Return Value

An [Auth Ticket Data](../types/auth-ticket-data.md) value

## Nodes

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
