---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Quick Start

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This simple scene outlines the basic steps to get up and running with Steamworks.

<figure><img src="../../../.gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure>

This is a bare bones scene that does nothing more than initialize the Steam API. The key component in the scene is the [Steamworks Behaviour](../components/steamworks-behaviour.md) located on the Manager game object.

You will also find an [Overlay Manager](../components/overlay-manager.md) on the same Manager game object which is simply demonstrating the use of Unity Events by virtue of the Using Unity Events sample script.

## Game Objects

### Manager

The manage game object has the [Steamworks Behaviour](../components/steamworks-behaviour.md) and [Overlay Manager](../components/overlay-manager.md) components attached and will handle initialization of the Steam API on start up based on the provided [Steam Settings](../scriptable-objects/steam-settings/) configuration. This is not the only way one can initialize Steam API but is simple and common approach used by many. You can learn more about Steam API initialization in the [Getting Started](../quick-start-guide/) article.

## Components

### [Steamworks Behaviour](../components/steamworks-behaviour.md)

The Steamworks Behaviour is a component script that can be added to a Game Object and configured with a Steam Settings object. This script will cause Steam API to be initialized on start and will initialize the Steam client or server endpoints as required based on the build target.

{% hint style="info" %}
In otherwords this will automatically initalize Steam for you\
Its smart enough to initalize the Client API for client builds and the Server API for server builds.
{% endhint %}

### [Overlay Manager](../components/overlay-manager.md)

The Overlay Manager is a component script that can be added to a Game Object to expose the common events related to Steam overlay. It is included here as a simple example of handling Steam related event via Unity Events.

### [User Profile](../prefabs/friend-profile.md)

![](<../../../.gitbook/assets/image (310).png>)

The User Profile present in the scene is simply here to prove to you that the Steam API is initialized and able to read data. On load it will fetch the local user's data and populate the avatar image, name, status, friend ID and Steam level.

{% hint style="info" %}
Note that your Steam level may not always load on first run. This is typical of this use case. That is reading a user's data immediately on start-up without first requesting user information.\
\
In a production use case you would generally request the information on bootstrap and not display it till some time later avoiding the timing issue you may see on first run in this sample scene.
{% endhint %}

## Testing

Assuming you are using an unmodified version of the sample scene and Steam Settings you will see messages appear in the Unity Editor Console log detailing each step of the initialization process.

<figure><img src="../../../.gitbook/assets/image (491).png" alt=""><figcaption><p>Example initialization messages</p></figcaption></figure>

In the event of an error details will be listed here along with troubleshooting guidance. In the event you require support please select the first error message in the log and press \[Ctrl + C] this will copy the full message and its stack trace to your clipboard. You can then paste that error into [Discord chat](https://discord.gg/eVVgM36) for live support or into a support email or similar.

Aside from the console output you will have a visual indication that Steam API is initialized correctly when your Steam User profile image, name, status and ID are displayed in the upper right corner of the screen.
