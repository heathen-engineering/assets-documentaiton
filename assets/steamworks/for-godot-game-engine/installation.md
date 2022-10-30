# Installation

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% embed url="https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Godot" %}
Steamworks Foundation for Godot on GitHub
{% endembed %}

## For New Projects

The [ProjectTemplate](https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Godot/Project%20Template) folder found on the GitHub repository is just that a project template. You can copy it down and edit it as a functional project and this is generally the best way to get started with a clean new project.

## For Existing Projects

1. Copy in the [Steamworks.NET](https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Godot/Project%20Template/Steamworks.NET) and [addons/Heathen](https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Godot/Project%20Template/addons/Heathen) folders into your project
2. Open Visual Studio (_or whatever code editor your using_) and add an assembly reference to the Steamworks.NET.dll located in the [Steamworks.NET](https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Godot/Project%20Template/Steamworks.NET) folder. \
   Obviously you should choose the Windows or OSX-Linux versions based on what platform your building for.
3. Enable the plugin in the editors Project Settings see the example below

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

This will have created the AutoLoad script Steamworks Behaviour for you

<figure><img src="../../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>
