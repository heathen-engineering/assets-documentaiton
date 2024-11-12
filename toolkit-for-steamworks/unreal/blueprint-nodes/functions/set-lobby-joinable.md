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

# 🔵 Set Lobby Joinable

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Sets whether or not a lobby is joinable by other players. This always defaults to enabled for a new lobby. If joining is disabled, then no players can join, even if they are a friend or have been invited. Lobbies with joining disabled will not be returned from a lobby search.

### Lobby Id

The id to set the value for

### Joinable

Should the lobby be made joinable (true) or not joinable (false)

### Return Value

True if successful, false if invalid lobby or you are not the owner of the lobby.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (11) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
