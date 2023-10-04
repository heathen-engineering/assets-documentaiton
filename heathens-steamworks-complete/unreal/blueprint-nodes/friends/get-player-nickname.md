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

# 🔵 Get Player Nickname

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Gets the nickname that the current user has set for the specified user.

### Id (input)

The ID of the user to get the nickname for.&#x20;

{% hint style="info" %}
The local user will never have a nickname.&#x20;

A nickname is the name the local user has assigned another user.&#x20;

For example let's assume your brother is your friend on Steam, and his chosen Steam Name is BroForce92, you could give him the nickname Little Bro; for you and only you the Get Player Nickname would return Little Bro for his user.&#x20;

You don't nickname yourself, when you set your name that is you setting your persona name.
{% endhint %}

### Return Value

**NULL** if no nickname has been set for that user.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (222).png" alt=""><figcaption></figcaption></figure>
