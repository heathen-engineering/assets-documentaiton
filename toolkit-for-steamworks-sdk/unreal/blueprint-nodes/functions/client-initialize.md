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

# 🔵 Client Initialize

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Initialize the Steam API.

This is only used for client builds, for server builds see the [Game Server Initialize](initialize.md) node.

### Return Value

**True** indicates that all required interfaces have been acquired and are accessible.\
**False** indicates one of the following conditions:

* The Steam client isn't running. A running Steam client is required to provide implementations of the various Steamworks interfaces.
* The Steam client couldn't determine the App ID of the game. If you're running your application from the executable or debugger directly then you must have a `steam_appid.txt` in your game directory next to the executable, with your app ID in it and nothing else. Steam will look for this file in the current working directory. If you are running your executable from a different directory you may need to relocate the `steam_appid.txt` file.
* Your application is not running under the same OS user context as the Steam client, such as a different user or administration access level.
* Ensure that you own a license for the App ID on the currently active Steam account. Your game must show up in your Steam library.
* Your App ID is not completely set up, i.e. in `Release State: Unavailable`, or it's missing default packages.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (716).png" alt=""><figcaption></figcaption></figure>
