---
description: Represents a group of firneds such as online, offline, etc.
---

# FriendGroup

## Overview

![](<../../../../.gitbook/assets/image (152).png>)

This is used by the [FriendGroups ](friendgroupsdisplay.md)component to&#x20;

## Inspector Fields

### Label

A Text element which will be the name of the group

### Counter

A Text element which will display the number of members in this group

### Toggle

A Toggle element used to expand or collapse this group

### Record Template

A GameObject that will be instantiated for each member in this group and parented to the "Content" refrence. This must implament a componenet which implaments the [IUserProfile ](../interfaces/iuserprofile.md)interface.
