---
description: Building and running a Steam game
---

# Running a Build

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

A typical Steam game is made dependent on the Steam client. This means that you must have Steam installed and running and logged in as a user that has access to the App Id your attempting to initialize as.&#x20;

### Build Testing

For proper build testing you should deploy your game to the Steam client preferably using the Content feature of [steamcmd.exe](https://partner.steamgames.com/doc/sdk/uploading) as found in the [Steam SDK](https://partner.steamgames.com/doc/sdk). You can set up test aka beta packages and add addition users for testing builds before the game its self is published live.

{% embed url="https://partner.steamgames.com/doc/store/testing#internal" %}
Setting up internal testers
{% endembed %}

### Dev Testing

While most dev testing is taken care of in Unity Editor you may also want to test a build without necessary bothering to upload it to Steam. To do this you \*\***must\*\*** include the [steam\_appid.txt](steam\_appid.txt.md) file in the root of the build.

## Troubleshooting

The following sections are just to help people find this information when searching in the Knowledge Base ... they all just point you to [steam\_appid.txt](steam\_appid.txt.md).

### Closes and relaunches from Steam

You ran your build without deploying it to Steam and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.

### Crash on Launch

You ran your build without deploying it to Steam and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.

### Tries to download Spacewar

You ran your build without deploying it to Steam and are using App ID 480 and  have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.
