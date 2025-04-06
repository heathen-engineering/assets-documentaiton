---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
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

# BP\_FriendsListGroup

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

This example blueprint is used with the [BP\_FriendsListDisplay](bp\_friendslistdisplay.md) to emulate the Steam Friends List look. It represents a "friend group" being a collection of friends organized either by tag or status.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (358).png" alt=""><figcaption></figcaption></figure>

</div>

The above image shows 2 such groups "Family" and "Online". This widget does not concern itself with sorting the users but rather expects you to provide it with a list of user IDs to display and a name to show in the header. For example "Family" and then the 3 IDs for Jodi, Maya and Kahlin.

## Construction

The widget has a custom event "Show Users" which when run will set the group name and iterate over the provided IDs

<figure><img src="../../../.gitbook/assets/image (359).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (360).png" alt=""><figcaption></figcaption></figure>

As we iterate over the provided IDs we create a new widget of type [BP\_FriendsListEntry ](bp\_friendslistentry.md)and pass it a specific User ID from the input array adding it to our Content Root which is a simple panel.

### Clear Children

To simplify clean up we did create a custom Clear Children function that does nothing more than clear the child widgets from our content root making it easy for a parent widget to trigger that process.
