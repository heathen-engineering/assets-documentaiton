---
description: Setting up the game
cover: ../../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Lobby Browser

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The Lobby Browser scene demonstrates a bare bones lobby browser set up.

<figure><img src="../../../../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

Lobby Browser is not a typical thing to do in modern game desing however it is an offten requested feature during the early development stages. The scene demonstrates the browsing and listing of lobbies, creating a lobby and leaving a lobby via UI elements.

### Features

#### Browse

Click the browse button to trigger a search of lobbies. This uses the [Lobby Manager's Search Arguments](../../ui-components/lobby-manager.md#searcharguments) to run and return the query and does not require any coding.

#### Create

Create a new lobby, this uses the [Lobby Manager's Create Arguments](../../ui-components/lobby-manager.md#createarguments) to create a new Steam Lobby and does not require any coding.

#### Leave

When in a lobby leave that lobby, this uses the [Lobby Manager's Leave](../../ui-components/lobby-manager.md#leave) method and does not require any coding.

#### Indicate when in a lobby

The Create/Leave button and the "You are in a Lobby" UI element are managed via the [events on the Lobby Manager](../../ui-components/lobby-manager.md#events) and do not require any coding.

## Components

### [Steamworks Behaviour](../../components/steamworks-behaviour.md)

The Steamworks Behaviour is a component script that can be added to a Game Object and configured with a Steam Settings object. This script will cause Steam API to be initialized on start and will initialize the Steam client or server endpoints as required based on the build target.

### [Lobby Manager](../../ui-components/lobby-manager.md)

This is what is doing all the work in terms of creating, searching, listing, leaving, etc. a Steam Lobby. It is located on the Manager game object.

### Lobby Browser UI Controller

{% hint style="info" %}
Sample Script

This is a sample script not meant for production use thus the "Deprecated" tag
{% endhint %}

This script is simply managing the sample scene's UI window responding the [Evt Found on the Lobby Manager](../../ui-components/lobby-manager.md#evtfound) to instantiate UI entries for each lobby reported. This is located on the Manager game object.

### Lobby Browser Lobby Record

{% hint style="info" %}
Sample Script

This is a sample script not meant for production use thus the "Deprecated" tag
{% endhint %}

This script is used on the template instantiated by the Lobby Browser UI Controller to display info about the specific lobby.

## Testing

Assuming you are using an unmodified version of the sample scene and Steam Settings you will see messages appear in the Unity Editor Console log detailing each step of the initialization process.

<figure><img src="../../../../.gitbook/assets/image (15) (1).png" alt=""><figcaption><p>Example initialization messages</p></figcaption></figure>

In the event of an error details will be listed here along with troubleshooting guidance. In the event you require support please select the first error message in the log and press \[Ctrl + C] this will copy the full message and its stack trace to your clipboard. You can then paste that error into [Discord chat](https://discord.gg/eVVgM36) for live support or into a support email or similar.

In addition as you browse, create, leave or join a lobby the console will report those actions along with any errors and troubleshooting guidance appropriate.
