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

# 🔵 Request User Information

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Requests the persona name and optionally the avatar of a specified user.

{% hint style="info" %}
It's slower to download avatars and churns the local cache, so if you don't need avatars, don't request them.
{% endhint %}

### User Id

The user to request the information for.

### Name Only

Retrieve the Persona name only (**true**)? Or both the name and the avatar (**false**)?

### Return Value

Triggers a [Persona State Change](../events/persona-state-change.md) callback.

**true** means that the data has been requested and a [Persona State Change](../events/persona-state-change.md) callback will be posted when it's retrieved.&#x20;

**false** means that we already have all the details about that user and functions that require this information can be used immediately.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>
