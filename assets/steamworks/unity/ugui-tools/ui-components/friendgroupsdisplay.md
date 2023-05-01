---
description: Funcitonaly similar to Steam Client's Friends List
---

# FriendGroupsDisplay

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

![](<../../../../../.gitbook/assets/image (176) (1).png>)

This control component is focused on emulation of Steam's own Friend List. It will read for and sort the local player's friends into the same list structure see in Steam Client's Friend List i.e. Playing, Online, Offline, any custom groups the player may have, etc.

This can be useful when you want a quick and easy UI element that the player is likely already familiar with.&#x20;

## Inspector Fields

### In Game Collection

This is a Transform which will be the root of all friends that are currently in or playing the current game.

### In Other Game Collection

This is a Transform which will be the root of all friends that are currently in or playing some other game.

### Grouped Collection

This is a Transform which will be the root of any custom groups the player may have defined.

### Online Collection

This is a Transform which will be the root of all friends that are currently online.

### Offline Collection

This is a Transform which will be the root of all friends that are currently offline.

### Group Prefab

This is a template or prefab that will be instantiated for each group found. i.e. Online, Offline, etc.

This GameObject must implement the [FriendGroup](friendgroup.md) component.

## Methods

### Clear

```csharp
public void Clear()
```

This simply destroys all loaded groups and profiles clearing the display. This is always called when the component is disabled.

### UpdateDisplay

```csharp
public void UpdateDisplay()
```

This simply rebuilds the display from scratch, that is it will first clear then re-construct the display insuring all elements are UpToDate. This is always called when the component is enabled.
