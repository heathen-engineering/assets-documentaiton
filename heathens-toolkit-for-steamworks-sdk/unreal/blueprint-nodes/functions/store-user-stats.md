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

# 🔵 Store User Stats

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
Only valid for Steam Game Servers
{% endhint %}

Send the changed stats and achievements data to the server for permanent storage for the specified user.\
\
If this fails then nothing is sent to the server. It's advisable to keep trying until the call is successful.\
\
This call can be rate-limited. Call frequency should be on the order of minutes, rather than seconds. You should only be calling this during major state changes such as the end of a round, the map changing, or the user leaving a server.\
\
If you have stats or achievements that you have saved locally but haven't uploaded with this function when your application process ends then this function will automatically be called.\
\
You can find additional debug information written to the `%steam_install%\logs\stats_log.txt` file.

### User

The user to store stats for

### Callback

An event delegate that will be executed when the process completes and will indicate the state and user.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
