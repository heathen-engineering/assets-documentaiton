# Quick Start

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This simple scene outlines the basic steps to get up and running with Steamworks.

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

This is a bare bones scene that does nothing more than initialize the Steam API. The key component in the scene is the [Steamworks Behaviour](../../unity/components/steamworks-behaviour.md) located on the Manager game object.

## Game Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../unity/components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

## Components

### [Steamworks Behaviour](../../unity/components/steamworks-behaviour.md)

The Steamworks Behaviour is the component responsible for initializing and operating the Steam API integration. It is important that this is initialized as soon as possible in your game and is never destroyed or duplicated.

it is \*\***strongly\*\*** recommended to use a [bootstrap design pattern](../../../../guides/design/bootstrap-scene.md) to insure that Steam API is initialized successful before even your main menu bothers to load.

### [Friend Profile](../../unity/ugui-tools/prefabs/friend-profile.md)

![](<../../../../.gitbook/assets/image (2) (4).png>)

The Friend Profile present in the scene is simply here to prove to you that the Steam API is initialized and able to read data. On load it will fetch the local user's data and populate the avatar image, name, status, friend ID and Steam level.
