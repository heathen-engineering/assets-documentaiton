---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# Game Instance

## Introduction

Heathen provides you with a ready to use Game Instance `BT_Steam_Game_Instnace` which is already configured to handle Steam API initialization for Client or Server builds and comes pre-configured with events to handle initialization, success or failure as well as restart required.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## Configuration

Defined as a Blueprint you can configure this instance to suit your needs by applying your App ID to the Steam Client Should Restart node

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

And if you planning on creating a server build you should also update the Steam Server Initialize node to suit your game's needs.

{% hint style="info" %}
Most games would read the server's configuration from command line arguments, an INI file or some similar external configuration point.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Events

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Shutdown, Should Restart, Failed Initialization and Initialization Complete are the core events you need to handle and the blueprint has them stubbed out for you.

{% hint style="info" %}
A default implementation for Shutdown, Should Restart and Failed to Initialize have been set up though for a good User Experience, you would likely want to expand on at least the Failed to Initialize to notify users of the failure.
{% endhint %}

### Bootstraping

The Bootstrap Your Game Here is the ideal place to warm up your game systems and runs right after Steam API has successfully initialized. This is where you would enable Steam Input, find your leaderboards, load system settings, read the player's inventory and initialise any additional game systems relevant to your game.
