---
cover: ../../../../.gitbook/assets/Unreal Banner@2x.png
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

# 🔵 Quick Match

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

A Heathen concept based on the most common use case of Steam Lobby.

In most cases, you want a player experience similar to that seen in DOTA, Halo, LOL, etc. where a player clicks a single button and the system finds a suitable match for them handling all aspects silently, aka a "quick match".

This process can be done manually by setting up a search, running the search if a result is found joining the top result, if no result is found creating a new lobby.

Heathen's Quick Match simply does the search, join and create in a single node for you. You would still create your search as you would any lobby request, call Quick Match when ready and its output will always include a lobby ID being either the found lobby it joined or a new lobby it created.

When Quick Match creates a lobby it does so as a private lobby with a max member limit of 2. You can then set your metadata as required, update your max member limit and then set your lobby to public or whatever other type you desire.

### Lobby ID

This will always be populated (unless you had an IO error or are a limited user). It will be the lobby you joined or the lobby you created.

### Created New

True if the process created a new lobby, false if it joined an existing one.

### Created Result

If a new lobby was created this is the [UEResult](../enumerators/ueresult.md) that Valve provided at the end of that process.

### Enter Blocked

If joining an existing lobby that blocked entry such as due to a ban or limited account this will be true otherwise false.

### Enter Response

If joining an existing lobby this will be the [UEChatRoomEnterResponse ](../enumerators/uechatroomenterresponse.md)that Valve returned at the end of that process.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (15) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
