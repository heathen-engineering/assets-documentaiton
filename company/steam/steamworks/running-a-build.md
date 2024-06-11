---
description: Building and running a Steam game
---

# 🏃 Running a Build

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

A typical Steam game is made dependent on the Steam client. This means that you must have Steam installed and running and logged in as a user that has access to the App Id your attempting to initialize as.&#x20;

### Build Testing

For proper build testing you should deploy your game to the Steam client preferably using the Content feature of [steamcmd.exe](https://partner.steamgames.com/doc/sdk/uploading) as found in the [Steam SDK](https://partner.steamgames.com/doc/sdk). You can set up test aka beta packages and add addition users for testing builds before the game its self is published live.

{% embed url="https://partner.steamgames.com/doc/store/testing#internal" %}
Setting up internal testers
{% endembed %}

### Dev Testing

While most dev testing is taken care of in Unity Editor you may also want to test a build without necessarily bothering to upload it to Steam. To do this you \*\***must\*\*** include the [steam\_appid.txt](steam\_appid.txt.md) file in the root of the build.

## Troubleshooting

The following sections are just to help people find this information when searching in the Knowledge Base ... they all just point you to [steam\_appid.txt](steam\_appid.txt.md).

### Closes and relaunches from Steam

This is a standard function of Steamworks aka "Restart if Required" it happens when the API detects it was not launched from the Steam client. It can be side-steped in a dev build for testing or for servers by proper use of the Steam AppId text file ... see the note below.

> You ran your build without deploying it to Steam and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.

### Crash on Launch

The most common cause of this

> You ran your build without deploying it to Steam and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.

For Unreal developers, the Steam AppId text file is still a requirement however you have a few more requirements owing to how Unreal integrates the Steamworks SDK with the engine. Make sure you have read and understand the [Getting Started](../../../toolkit-for-steamworks/unreal/getting-started.md) guide!

Even if you are not using OnlineSubsystemSteam you do require its configuration values because that is where Epic Games decided to define the config required. Also, be aware of the definitions you require in order to initialise the API correctly. In Editor, we will handle this for you but in a build you need to have this done properly.

### Tries to download Spacewar

You ran your build without deploying it to Steam and are using App ID 480 and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.
