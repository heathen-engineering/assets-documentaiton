---
description: Understanding the core of Heathen's Steamworks SDK
---

# Steamworks Behaviour

## Introduction

Steamworks Behaviour is the main component to the Steamworks SDK, and handles initialization of the Steam API and processing of the API's callbacks.&#x20;

{% hint style="warning" %}
Every game must have 1 and only 1 of these objects that should be initialized at the start and never destroyed nor re-initialized.
{% endhint %}

It is very important that your game initializes the Steamworks Behavior before making any operations against the Steam API. It is just as important that your game never attempts to initialize more than 1 Steamworks Behavior

{% hint style="danger" %}
A common problem with many Unity projects is the use of Do Not Destroy on load as a compensation for bootstrapping the game.

This concept needs its own dedicated article so please [read more here](https://kb.heathenengineering.com/assets/ux/concepts/bootstrap-scene)!
{% endhint %}

## Usage

The most common use is to simply add the Steamworks Behavior Component to an appropriate game object and reference your Steam Settings.

![](<../../../.gitbook/assets/image (73).png>)

As noted it is highly important that you do not destroy this object and that you never initialize a second copy of this object.

### What not to do

* **DO NOT**\
  Create a Steamworks Behavior in every scene
* **DO NOT**\
  Reload a scene that defines Steamworks Behavior; for example **do not** define Steamworks Behavior in your Title scene, because you will load and reload that scene many times
* **DO NOT **\
  Destroy the game object where Steamworks Behavior is defined
* **DO NOT**\
  Use Steamworks' SteamManager. Steamworks SteamManager should not even be defined in your game project. The Steamworks SteamManager is an example script from Steamworks.NET, it is not suitable for production use, it does not support Steam Game Server intialization and all of its relivent funcitonality is handled by Heathen's Steamworks Behavior.
* **DO NOT**\
  Apply both Steamworks Behavior and Steamworks Creator to the same game object.&#x20;
* **DO NOT **\
  Use both Steamworks Behavior and Steamworks Creator. That is you should have 1 or the other in your project never both.

### What to do

* **DO**\
  Create the Steamworks Behavior in a scene that loads in your game first before any other scene&#x20;
* **DO**\
  Insure that the game object you defined Steamworks Behavior on is never destroyed. You can do that by either using additive loading and simply never unloading your "bootstrap" scene, or you can mark the game object you applied the Steamworks Behavior to as Do Not Destroy On Load. This will create a hidden scene and will move the object there. If you do this (use Do Not Destroy On Load) it is **VERY **important that you never reload the scene where Steamworks Behavior was initally defined.



