# Debugging Steam API

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
Steam's Documentation has a Debugging article as well ... read it ... its good

[https://partner.steamgames.com/doc/sdk/api/debugging](https://partner.steamgames.com/doc/sdk/api/debugging)
{% endhint %}

Follows are a few common issues and solutions as well as additional notes on the debugging tools available to you both from Heathen and Valve.

## Enable Debugging

![Toggle this on](<../../../.gitbook/assets/image (3) (1).png>)

When toggled on Heathen's tools will write additional verbose information in particular around initialization which is the most common point of error. If you have not finished testing and are not building a fully tested, production ready, release build ... then you should have this turned on.

## Steam must be running

Be aware that none of the work done by Steam API is "in" your game, Steam API is an "application program interface" that allows your game to work with features in the Steam client. As a result you **must** have Steam client open, running and logged in to a valid Steam user that owns the app you are trying to work with.

The only exception to this is when using the [Steam Game Server](../features/multiplayer/game-server-browser.md) feature which also limits the functionality of Steam API as there is no client and no user available to do work.

## Running a Build&#x20;

When running a build that was not deployed to Steam and ran from the Steam client you will notice that the game fails to initialize the crashes to desktop possibly attempting to re-launch from Steam client.

This is by design, you must hint to Steam API what the app is, read the [article on steam\_appid.txt](debugging-steam-api.md#steam\_appid.txt) it will explain, why this happens, how to work with it, when you should and when you should not use the feature described.

## Publish Your Changes

When you make any changes in Steam Developer Portal you **must** publish them before they take effect and can be testing in your game

> Use this page to publish all of the metadata that you've used this site to author. You'll need to publish in order to test things like your game **depot configuration**, new builds, or new **achievements** you've added. If your game is not yet set to playable, this action **will not release the game**, but will simply **publish configuration changes you've made**.
>
> \
> The buttons below invoke source control (Perforce) commands - if you have any trouble with these, just let us know.

The above quote is from the publish page as seen below

![The publish page, make sure to publish before you try to test](<../../../.gitbook/assets/image (164).png>)

## Environment Checks

Having something wrong with your environment (Unity Editor, Steam.exe, Steam User, etc.) can cause odd issues with Steam API ones that are hard to pin down unless you know what to look for.

Here are some key things to check before you bother trying to debug anything.

### Steamworks.NET Install

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

## Steam Command Line

{% embed url="https://partner.steamgames.com/doc/sdk/api/debugging" %}
Tools from Valve
{% endembed %}

> Steam has grown into a large application over the years and provides many separate modules and multiple different ways to debug. This page outlines as many of them as possible to help you get the most out of Steam and Steamworks while keeping headaches to a minimum.\
> \
> Steam automatically outputs a number of debug to the `logs` folder, for others you may need to use [Steam Command Line Parameters](https://partner.steamgames.com/doc/sdk/api/debugging#command\_line\_parameters) or [Steam Console Commands](https://partner.steamgames.com/doc/sdk/api/debugging#console\_commands) to enable them.\
> \
> Using [ISteamUtils::SetWarningMessageHook](https://partner.steamgames.com/doc/api/ISteamUtils#SetWarningMessageHook) allows a Steamworks application to register a function that allows the Steamworks API to provide human-readable error messages to the application when something goes wrong. Most Steam APIs use it, so be sure to hook it up and look at it any time something goes wrong.

## Steamworks Inspector

Heathen provides a powerful inspector that will show you the states and values of all Steam API artefacts configured for your project.&#x20;

To Access the inspector simply open the **Window > Steamworks Inspector** menu.

or

![Click the button in Steam Settings](<../../../.gitbook/assets/image (5).png>)

{% hint style="warning" %}
#### IMPORTANT

The inspector's data only populate while the simulation is running.
{% endhint %}

The Home page of the inspector displays core values for your user and the app its self. This is the first place you should check, and you should do the following

1. Is the Initialization Status = Initialized?
2. Is the Listed App ID what I expect it to be?
3. Is the Reported App ID the same as the Listed App ID
4. Is the steam\_appid.txt the same as the Listed App ID
5. Is the displayed user me / who I expect it to be

![](<../../../.gitbook/assets/image (151) (1).png>)

If you answered no to any of the above questions your issue is on step 1. That is your not configured correctly to initialize Steam and or you do not have the Steam client up and running with a valid user logged in.

If for example you find that the App ID does not match then what you most likely did was to change the App ID in the Steam Settings file but did not fully shut down Unity, Visual Studio and absolutely everything else that might have mounted it; e.g. Unity, Visual Studio or any related process.

The reason this happens is that Valve will not release app initialization until every process that mounted its handles has closed. This is the single most common issue we have reported.

### Initialization Status

This indicates the status of the Steam API and will have one of the following values

* Idle\
  This means the API is not, nor has it attempted to initialize. The status will say this anytime the simulation is not running ... that is you must press play for this to work at all.
* Initializing\
  This means the API is trying to initialize, this generally happens very fast so you may never see this.
* Initialized\
  This means the API is initialized and that the values reported are as reported by the API
* Error or Failed\
  This means the API failed to initialize, check your Unity Editor console log for details as to why

### Listed App ID

This is the App ID that appears in the active Steam Settings object. It should match the other listed IDs

### Reported App ID

This is the App ID that Steam API has reported back to us when asked. As far as Steam is concerned this is the App ID you "**are**"

### Steam\_AppId.txt

This is the App ID that is currently recorded in the steam\_appid.txt file

### Inspecting Stats

![](<../../../.gitbook/assets/image (173) (1) (1).png>)

You can use the Stats tab to view and update the value of all registered stats

### Inspecting Achievements

![](<../../../.gitbook/assets/image (179) (1) (1) (1) (1).png>)

You can use the Achievements tab to view and unlock/reset all registered achievements

### Inspecting Leaderboards

![](<../../../.gitbook/assets/image (170) (1) (1) (1) (1).png>)

You can use the Leaderboard's tab to view your score and rank on all registered leaderboards. Leaderboards while one of the simplest aspects of Steam API are also one of the more fragile aspects.

Common issues seen with Leaderboards include

1. You have the sort order set incorrectly
2. You have the leaderboard set to trusted only
3. You made changes in Steam Developer Portal and didn't publish them

We do on occasion see leaderboards "break", this is typically a problem when you change values on the board or delete a board and make a new one with the same name but different settings. In most cases its easiest and best to simply make a new board with a new unique API name.&#x20;

If you need to repair a board that is misbehaving you will need to contact Valve's support as these are backend features Heathen can not see nor effect.

### Inspecting Downloadable Content

![](<../../../.gitbook/assets/image (181) (1) (1) (1).png>)

You can view the subscription status of all DLC in the DLC tab

### Inspecting Inventory

![](<../../../.gitbook/assets/image (164) (1) (1) (1) (1) (1) (1).png>)

The inventory tab will display all the items registered to your game and provides tools for clearing and granting each item

### Inspecting Lobbies

![](<../../../.gitbook/assets/image (185) (1).png>)

The lobbies tab will populate a sub page for each detected lobby and will display the list of members and the lobby's metadata.
