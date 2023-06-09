---
description: How to .... everything!
---

# ⚙ Steamworks

## Steam Debugging

{% hint style="info" %}
Steam's Documentation has a Debugging article as well ... read it ... its good

[https://partner.steamgames.com/doc/sdk/api/debugging](https://partner.steamgames.com/doc/sdk/api/debugging)
{% endhint %}

The following articles will help you learn how to perform common tasks and to debug and troubleshoot your Steam API integration. We have created a large array of tools that simplify the use of Steam API including tools like Steamworks Inspector to help you troubleshoot and debug your integration.

## The Basics

### Steam must be running

Be aware that none of the work done by Steam API is "in" your game, Steam API is an "application program interface" that allows your game to work with features in the Steam client. As a result you **must** have Steam client open, running and logged in to a valid Steam user that owns the app you are trying to work with.

The only exception to this is when using the [Steam Game Server](multiplayer/game-server-browser/) feature which also limits the functionality of Steam API as there is no client and no user available to do work.

### Running a Build&#x20;

When running a build that was not deployed to Steam and ran from the Steam client you will notice that the game fails to initialize the crashes to desktop possibly attempting to re-launch from Steam client.

This is by design, you must hint to Steam API what the app is, read the [article on steam\_appid.txt](steam\_appid.txt.md) it will explain, why this happens, how to work with it, when you should and when you should not use the feature described.

### Publish Your Changes

When you make any changes in Steam Developer Portal you **must** publish them before they take effect and can be testing in your game

> Use this page to publish all of the metadata that you've used this site to author. You'll need to publish in order to test things like your game **depot configuration**, new builds, or new **achievements** you've added. If your game is not yet set to playable, this action **will not release the game**, but will simply **publish configuration changes you've made**.
>
> \
> The buttons below invoke source control (Perforce) commands - if you have any trouble with these, just let us know.

The above quote is from the publish page as seen below

![The publish page, make sure to publish before you try to test](<../../../.gitbook/assets/image (164).png>)

### Environment Checks

Having something wrong with your environment (Engine Editor, Steam.exe, Steam User, etc.) can cause odd issues with Steam API ones that are hard to pin down unless you know what to look for.

Here are some key things to check before you bother trying to debug anything.

### Steamworks.NET Install

{% hint style="info" %}
Issue present in Unity only
{% endhint %}

Did you **ever** have a manual or custom installation of Steamworks.NET or ever have any asset or tool that had such in your project?

That is at any time was there ever a Steamwork.NET in your project that was not from the Package Manager Git URL install?

If yes; then know that those custom installs would have Steamworks.NET artefacts in multiple folder locations. If that install was present or even partially present from an incomplete attempt to manually remove it then Unity will have ... on install of the proper Steamworks.NET from Package Manager ... attempted to merge the assets and made a complete mess of it.

#### How to fix

1. Remove the offending files\
   Steamworks.NET manual installs would have installed bits in several different folders (scripts, plugins, examples, etc.)\
   Many old assets would have buried a copy or customized version of Steamworks.NET in there asset.
2. Once you are positive that you fully remove Steamworks.NET and related files from your Assets folder.\
   Remove Steamworks.NET from package manager and then reinstall it

### Steam Client Login

For some reason some devs like to run Steam.exe as Admin or run Unity Editor as Admin ... Windows will mangle your callbacks if you do this.

Its important that Unity Editor and Steam.exe are running as the same user, which should also be the user that is logged into the OS  in order for Steam API to work properly.

e.g. Do not run either Steam.exe or Unity Editor with elevated or any other non-standard permissions or users. If you do you will have issues.

### Steam User

Valve's Steam has a concept of "limited" users ... when a new user is created it is considered limited until it has spent the equivalent of 5 USD on the Steam store or added 5 USD to the Steam wallet.

This applies to dev accounts, publishers, etc. there are no exceptions. So if your account or your test account is new and or has not spent at least 5 USD on Steam odds are its limited by Valve and it will have limited access to Steam API including but not limited to&#x20;

* Lobby limits\
  Can join but cant really use a Steam Lobby ... this one is real odd as it will join it but it cant do anything beyond that
* Chat limits\
  Typically cant chat with anyone
* Friend limits\
  Typically cant have friends, friend chats, friend invites, etc.

In addition the Steam User your testing the game with MUST own a license to the app to initialize the Steam API. Developer accounts are "supposed" to be granted a dev license to the app ... however we have seen it such that this doesn't happen correctly.

You can test and modify ownership of the app you are a dev for using Steam's command line as outlined in&#x20;

{% embed url="https://partner.steamgames.com/doc/sdk/api/debugging" %}

### Build Target

Steamworks.NET and as a result all related Steam code is only applicable to PC, Mac and Linux ... not Universal Windows or anything else ... ONLY ... Windows 32, Windows 64, Max OS and Linux 64 platforms.&#x20;

If your build target is set to ANY other build target then the Steamworks.NET assembly will not compile and will not be available for use.

#### What about multi-platform games?

use `#if DISABLESTEAMWORKS` script define you can add this your self if you like to cause Steam API code to simply not compile. You can use it to strip out your Steam related code if you need.

### Steam Command Line

{% embed url="https://partner.steamgames.com/doc/sdk/api/debugging" %}
Tools from Valve
{% endembed %}

> Steam has grown into a large application over the years and provides many separate modules and multiple different ways to debug. This page outlines as many of them as possible to help you get the most out of Steam and Steamworks while keeping headaches to a minimum.\
> \
> Steam automatically outputs a number of debug to the `logs` folder, for others you may need to use [Steam Command Line Parameters](https://partner.steamgames.com/doc/sdk/api/debugging#command\_line\_parameters) or [Steam Console Commands](https://partner.steamgames.com/doc/sdk/api/debugging#console\_commands) to enable them.\
> \
> Using [ISteamUtils::SetWarningMessageHook](https://partner.steamgames.com/doc/api/ISteamUtils#SetWarningMessageHook) allows a Steamworks application to register a function that allows the Steamworks API to provide human-readable error messages to the application when something goes wrong. Most Steam APIs use it, so be sure to hook it up and look at it any time something goes wrong.
