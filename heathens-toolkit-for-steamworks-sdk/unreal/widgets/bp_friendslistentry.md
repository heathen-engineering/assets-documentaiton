---
cover: ../../../.gitbook/assets/Unreal Banner@2x.png
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

# BP\_FriendsListEntry

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

A simple widget to display a user's avatar, name and status is used by the [BP\_FriendsListGroup ](bp\_friendslistgroup.md)and further by the [BP\_FriendsListDisplay](bp\_friendslistdisplay.md).

<figure><img src="../../../.gitbook/assets/image (361).png" alt=""><figcaption></figcaption></figure>

## Construction

<figure><img src="../../../.gitbook/assets/image (362).png" alt=""><figcaption></figcaption></figure>

This simple example widget has a single event Set User Data which takes in a User ID and uses that to set the user's image, name and status. Note that this widget example uses the [BP\_SteamAvatarImage ](bp\_steamavatarimage.md)and [BP\_SteamUserName ](bp\_steamusername.md)widgets to further simplify getting and displaying name and image.
