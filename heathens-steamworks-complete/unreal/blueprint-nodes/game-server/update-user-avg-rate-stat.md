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

# 🔵 Update User Avg Rate Stat

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

Updates an AVGRATE stat with new values for the specified user.

You must have called [Request User Stats](request-user-stats.md) and it needs to return successfully via its callback prior to calling this!

This call only modifies Steam's in-memory state and is very cheap. To submit the stats to the server you must call Store User Stats.

{% hint style="info" %}
This will work only on achievements that game servers are allowed to set. If the "Set By" field for this achievement is "Official GS" then only game servers that have been declared as officially controlled by you will be able to set it. To do this you must set the IP range of your official servers in the [Dedicated Servers](https://partner.steamgames.com/apps/dedicatedservers/) section of App Admin.
{% endhint %}

### User

The Steam ID of the user to update the AVGRATE stat.

### API Name

The API Name of the stat

### Value

The value accumulation since the last call to this function

### Length

The amount of applicable time in seconds since the last call to this function

### Return Value

True if successful

## Nodes

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
