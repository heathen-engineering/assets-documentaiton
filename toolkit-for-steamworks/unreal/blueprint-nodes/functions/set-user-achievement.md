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

# 🔵 Set User Achievement

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
Only valid for Steam Game Servers
{% endhint %}

Unlocks an achievement for the specified user.

You must have called [Request User Stats](request-user-stats.md) and it needs to return successfully via its callback prior to calling this!

This call only modifies Steam's in-memory state and is very cheap. To submit the stats to the server you must call Store User Stats.

{% hint style="info" %}
This will work only on achievements that game servers are allowed to set. If the "Set By" field for this achievement is "Official GS" then only game servers that have been declared as officially controlled by you will be able to set it. To do this you must set the IP range of your official servers in the [Dedicated Servers](https://partner.steamgames.com/apps/dedicatedservers/) section of App Admin.
{% endhint %}

### User

The user to set the achievement for

### API Name

The API Name of the Achievement to set

### Return Value

True if successful

## Nodes

<figure><img src="../../../../.gitbook/assets/image (298).png" alt=""><figcaption></figcaption></figure>
