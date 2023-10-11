---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Getting Started

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Your first step is to initialize the Steam API and we give you a few options to do just that.

* Steam Game Instance\
  A pre-configured Blueprint of type Game Instance, simply apply it and move on
* Blueprint Nodes\
  Easy-to-use blueprint nodes you can add to your existing initialization process
* C++\
  The full features of Steam API available C++

## Steam Game Instance

<figure><img src="../../.gitbook/assets/image (299).png" alt=""><figcaption></figcaption></figure>

A premade Blueprint of type Game Instance that handles initialization and shutdown of Steamworks APIs for both Client and Server builds.

The expectation is that you will open up and modify this Blueprint to suit your game's needs.

### App ID

<figure><img src="../../.gitbook/assets/image (300).png" alt=""><figcaption></figcaption></figure>

Your first step should be to set your App ID in the Steam Client Should Restart node. This will be used by Steamworks to hint and test whether or not the app should be restarted from Steam client.

In the event the test is true the Should Restart event will be called, otherwise Client Initialization will proceed.

### Game Server Configuraiton

<figure><img src="../../.gitbook/assets/image (302).png" alt=""><figcaption></figcaption></figure>

If your game will have a dedicated server build you should update the Steam Server Initialization node according to your configuration. The specifics of how you do this and what you will set the values to will depend on the nature of your servers, how they are hosted and how they are allocated.

For example, if your servers are allocated dynamically you may want to pass the required information in on the command line in that case you could read parameters from the command line to populate the required fields. Unreal's built-in tools can help you with this

<figure><img src="../../.gitbook/assets/image (303).png" alt=""><figcaption></figcaption></figure>

### Bootstrap

<figure><img src="../../.gitbook/assets/image (304).png" alt=""><figcaption></figcaption></figure>

The concept of "bootstrapping" is a common one and pre-configured in the sample. The Initialization Complete even will be raised when Steam is ready to use and you can easily apply any additional logic you require at this time to ensure that the user does own the game and that the API is ready to be used.

For example, this would be the ideal time to load system settings, user profiles and other saved data from Steam Remote Storage.

## Blueprint

You will probably want to initialize and run your Steam integration globally at the level of the whole game as opposed to linking it to a given object or actor.

For that reason, we recommend you use "Game Instance" as the base class of a new blueprint. Don't forget to set your new Game Instance in the Project Settings.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Open your new blueprint and let's create a few nodes

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The above shows a fully functional initialization, update and shutdown of the Steam API all connected to your game's lifecycle from a blueprint.

Let's go over what each node is and does

### Event Init

This is part of the Game Instance base class and happens when the game first initialises. From here we are simply going to call `Steam Client Should Restart`

### Steam Client Should Restart

This expects you to provide your Steam App ID as input, this is a value of type int32.

This does 2 important things.

1. When running in the editor this will check for and add the steam\_appid.txt if missing.
2. At run time this will check for said file and if missing it will check for launch from Steam and if not it will try to launch the game from Steam.

This node returns a bool and if true it means we need to close this game because it's going to be relaunched from the Steam client.

Learn more about [steam\_appid.txt](../../company/steam/steamworks/steam\_appid.txt.md), when it should be used and when it should NOT be used.

### If True: Quit Game

If true we use the Quit Game node and let the game close.

### If False: Steam Client Initialize

This node initializes the Steam Client API ... note Client and Server are two different endpoints. In this example, we are only dealing with clients. If you wanted to deal with the server as well you would need to test ... is a server or client build and use the appropriate Steam XXXX Initialize.

This node returns a bool which we will test

### If True: Set Timer by Event

If the initialization returned true then we want to start a loop that will check for updates to Steam Callbacks. Drag the event node off and link it to a Steam Client Run Callbacks.

### Steam Client Run Callbacks

This runs Valev's Steam Callbacks which is what causes events to invoke backend forth between your game and the Steam client

### If False: \<Handle Failure>

If the Steam Client Initialize fails it will return false. This will only fail if one of the following is true.

* The API doesn't know what App it is. This happens when it's not launched from the Steam client and there is no steam\_appid.txt
* Your game can not mount the Steam client. By that, we mean the Steam client and your game are running in different contexts and can't talk. Such as if the user ran the game or Steam client as admin or similar.
* The user doesn't own a valid license to the App ID in question.

In this case, you should notify your user of the issue and probably shut the game down assuming the game is dependent on Steam or that otherwise you only want a valid Steam user who owns your game to play the game.

## C++

{% hint style="warning" %}
WIP Document

The instructions for C++ are the same for native C++ so you can use Valve's own documentation for that ... for now ... we will eventually write our own to a better experience for you.\
\
For now, here is how you include the steam\_api.h with our plugin installed.

```
#include <SteamworksComplete/sdk/steam_api.h>
```
{% endhint %}
