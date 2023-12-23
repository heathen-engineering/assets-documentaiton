---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Game Server Browser

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This scene demonstrates the use of the [Steam Game Server Browser](game-server-browser.md) feature.

<figure><img src="../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

## Components

### [Steamworks Behaviour](../components/steamworks-behaviour.md)

The Steamworks Behaviour is a component script that can be added to a Game Object and configured with a Steam Settings object. This script will cause Steam API to be initialized on start and will initialize the Steam client or server endpoints as required based on the build target.

{% hint style="info" %}
In otherwords this will automatically initalize Steam for you\
Its smart enough to initialize the Client API for client builds and the Server API for server builds.
{% endhint %}

### [Game Server Browser Manager](../components/game-server-browser-manager.md)

This behaviour simplifies working with Steam Game Server queries and exposes the resulting response as a Unity Event.

### Game Server Browser UI Controller

{% hint style="info" %}
Sample Script

This is a sample script not meant for production use thus the "Deprecated" tag
{% endhint %}

A demo script that is controlling the UI elements only.
