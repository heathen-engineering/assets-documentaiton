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

# 🔵 Logged On

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Check if the current user's Steam client is connected to the Steam servers.\
\
If it's not then no real-time services provided by the Steamworks API will be enabled. The Steam client will automatically be trying to recreate the connection as often as possible. When the connection is restored a [Servers Connected](../events/servers-connected.md) callback will be posted.\
\
You usually don't need to check for this yourself. All of the API calls that rely on this will be checked internally. Forcefully disabling stuff when the player loses access is usually not a very good experience for the player and you could be preventing them from accessing APIs that do not need a live connection to Steam.

### Return Value

**true** if the Steam client currently has a live connection to the Steam servers; otherwise, **false** if there is no active connection due to either a networking issue on the local machine, or the Steam server is down/busy.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (825).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (793).png" alt=""><figcaption></figcaption></figure>
