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

# 🔵 Client Should Restart

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Test if the app was launched from the Steam client, if it was not it will attempt to launch the app from the Steam client and will return true on the Return Value.

### App Id (Input)

The App ID is to be tested, if the user does not own the app the Steam Store page for the app will be opened. If the user does own the app but the app was not launched from the Steam client then the app will be launched from the Steam client.

* If steam\_appid.txt is present it will cause this test to skip, you should not ship the steam\_appid.txt with your game. It is for dev use and use with Steam Game Server. See the article on [steam\_appid.txt](../../../../company/steam/steamworks/steam\_appid.txt.md) for more information.

### Return Value

True if the app needs to be restarted. In this case Steam will be launching the game so you should clean up and shutdown this copy of the game.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>
