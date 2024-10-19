---
description: Represents a group of friends such as online, offline, etc.
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Friend Group

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

![](<../../../../.gitbook/assets/image (152).png>)

This is used by the [FriendGroups ](friend-groups-display.md)component when instantiating groups in the list. The FriendGroup is responsible for instantiating each user record within it and maintaining that information.

## Inspector Fields

### Label

A Text element which will be the name of the group

### Counter

A Text element which will display the number of members in this group

### Toggle

A Toggle element used to expand or collapse this group

### Record Template

A GameObject that will be instantiated for each member in this group and parented to the "Content" reference. This must implement a component which implements the [IUserProfile ](../programming-tools/iuserprofile.md)interface.
