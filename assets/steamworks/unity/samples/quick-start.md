# Quick Start

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

This simple scene outlines the basic steps to get up and running with Steamworks.

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

This is a bare bones scene that does nothing more than initialize the Steam API. The key component in the scene is the [Steamworks Behaviour](../components/steamworks-behaviour.md) located on the Manager game object.

## Game Objects

### Manager

The manage game object has the [Steamworks Behaviour](../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

## Components

### [Steamworks Behaviour](../components/steamworks-behaviour.md)

The Steamworks Behaviour is the component responsible for initializing and operating the Steam API integration. It is important that this is initialized as soon as possible in your game and is never destroyed or duplicated.

it is \*\***strongly\*\*** recommended to use a [bootstrap design pattern](../../../../company/concepts/design/bootstrap-scene.md) to insure that Steam API is initialized successful before even your main menu bothers to load.

### [Friend Profile](../ugui-tools/prefabs/friend-profile.md)

![](<../../../../.gitbook/assets/image (2).png>)

The Friend Profile present in the scene is simply here to prove to you that the Steam API is initialized and able to read data. On load it will fetch the local user's data and populate the avatar image, name, status, friend ID and Steam level.
