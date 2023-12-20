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

# 🔵 Leave Lobby

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Leave a lobby that the user is currently in; this will take effect immediately on the client side, other users in the lobby will be notified by a [Lobby Chat Update](../events/lobby-chat-update.md) callback.

### Lobby Id

The Steam ID of the lobby to invite the user to

### Callback

An event that will be called when the process completes and will indicate the results of the request.

* Lobby Id\
  The lobby joined
* User Changed\
  The user the change applies to
* User Made Change\
  The user that caused the change
* State Change\
  The [UEChatMemeberStateChange](../enumerators/uechatmemberstatechange.md) value

## Nodes

<figure><img src="../../../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>
