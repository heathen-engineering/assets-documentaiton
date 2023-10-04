---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Steam Game Server

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This scene is used to demonstrate Steam Game Server initialization. This doesn't actually require any special coding or components and is handled through the Steamwork Behaviour automatically for you based on your build target such that any server build will simply initialize the API as a Steam Game Server according to your [Steam Settings](../scriptable-objects/steam-settings/).

<figure><img src="../../../.gitbook/assets/image (13) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Components

### [Steamworks Behaviour](../components/steamworks-behaviour.md)

The Steamworks Behaviour is a component script that can be added to a Game Object and configured with a Steam Settings object. This script will cause Steam API to be initialized on start and will initialize the Steam client or server endpoints as required based on the build target.

{% hint style="info" %}
In otherwords this will automatically initalize Steam for you\
Its smart enough to initialize the Client API for client builds and the Server API for server builds.
{% endhint %}

## Testing

Assuming you are using an unmodified version of the sample scene and Steam Settings you will see messages appear in the Unity Editor Console log detailing each step of the initialization process.

<figure><img src="../../../.gitbook/assets/image (19) (1) (1).png" alt=""><figcaption></figcaption></figure>

In the event of an error details will be listed here along with troubleshooting guidance. In the event you require support please select the first error message in the log and press \[Ctrl + C] this will copy the full message and its stack trace to your clipboard. You can then paste that error into [Discord chat](https://discord.gg/eVVgM36) for live support or into a support email or similar.

As you read over the consome messages you will that the final step reports the status of the server and the Server's issues Steam ID. It is that Steam ID that would be used to connect with Steam Networking Sockets for Client / Server based networking.
