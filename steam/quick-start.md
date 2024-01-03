---
description: Taking your very first step!
---

# ☝ Quick Start

{% hint style="success" %}
#### Like what you're seeing?

Consider supporting us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools, and assets, escalated support and issue tracking, and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Your first step is to navigate to [partner.steamworks.com](https://partner.steamgames.com/) we strongly recommend you create a new Steam account to represent you as a publisher or developer separate from any personal account/s you might have. Remember, new Steam accounts start as "limited" Put $5 in your Steam wallet to get around this.&#x20;

{% embed url="https://partner.steamgames.com/" %}
Step 1
{% endembed %}

Steamworks has its very own [Getting Started](https://partner.steamgames.com/doc/gettingstarted) guide ... read it and follow it

{% embed url="https://partner.steamgames.com/doc/gettingstarted" %}
Read this ... do as it says
{% endembed %}

## Sign-up to Steamworks

If you read the [getting started article](https://partner.steamgames.com/doc/gettingstarted) linked above and followed its instructions you should have already been guided to pay the [Steam Direct fee](https://partner.steamgames.com/doc/store/application) which will get you your first App ID.

### Do I need it to get started?

Technically ... for the very first step ... no.\
In reality absolutely yes, you can't do anything meaningful without your App ID.

You can test some features of Steam API using the test application "Spacewars" whose app ID is 480. This is the app ID we use in all of our [Steamworks](../toolkit-for-steamworks-sdk/steamworks.md) sample scenes and doesn't require you to be signed up to use it.

Having said that you can't do anything meaningful with the test app, it exists as a teaching tool. To create the stats, achievements, leaderboard, workshop, etc. for your game you will require an App ID and we do recommend you do this as soon as you are sure you want to release your game on Steam ... no reason to wait.

## Steam API

Once you're all set up as a Steam Developer and have your App ID your next step should be to get familiar with the Steam API and what it has to offer. Heathen creates the best Steam integration for Unreal, Unity and Godot, read more on our [Steamworks page](../toolkit-for-steamworks-sdk/steamworks.md).

Steam API is of tremendous value especially for small and indie developers as it is a power set of backend services and is completely free for you to use. We strongly recommend you understand what Steam API can do for your game before you commit your design. The best and most successful games fully exploit Steam's features.

### Tools

Heathen's Toolkit for Steamworks SDK is the best tool for Valve's Steamworks SDK in Unreal, Unity or Godot (preview). The tool has been maintained and updated for more than a decade, is trusted by thousands of developers and drives hundreds of games on Steam. Toolkit for Steamworks is more than just an API wrapper and includes engine-specific tools and systems on top of a complete integration of Valve's Steam APIs.

<figure><img src="../.gitbook/assets/Short Banner@2x.png" alt="Steamworks Complete"><figcaption></figcaption></figure>

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Complete</td><td><a href="https://github.com/sponsors/heathen-engineering">GitHub | Patreon</a></td><td><a href="https://www.unrealengine.com/marketplace/en-US/product/ad658ddf5c434478acb95f9091ea279c">Marketplace</a></td><td><a href="../.gitbook/assets/UnrealCardCover.png">UnrealCardCover.png</a></td><td><a href="../toolkit-for-steamworks-sdk/unreal/">unreal</a></td></tr><tr><td>Complete | Foundation</td><td><a href="https://github.com/sponsors/heathen-engineering">Gitub | Patreon</a></td><td><a href="https://assetstore.unity.com/packages/tools/integration/steam-api-steamworks-complete-246652">Asset Store</a></td><td><a href="../.gitbook/assets/UnityCardCover.png">UnityCardCover.png</a></td><td><a href="../toolkit-for-steamworks-sdk/unity/">unity</a></td></tr><tr><td>Foundation</td><td><a href="https://github.com/heathen-engineering/SteamworksFoundation">GitHub</a></td><td></td><td><a href="../.gitbook/assets/GodotCardCover.png">GodotCardCover.png</a></td><td><a href="../toolkit-for-steamworks-sdk/godot/">godot</a></td></tr></tbody></table>

## Unlearning Bad Habits

Unfortunately, there is a lot of just bad samples and example code out there, especially around Steamworks / Steam API for Unity. Even Unreal's own built-in Online Subsystem Steam and Steam Sockets plugins are very out-of-date and make some odd uses of the API that do not align with "good practice" as defined by Valve. Here are some common things you might have picked up or learned that you should throw out right now.

### Unreal's Online Subsystem Steam

1st understand what an Online Subsystem is. ... TL;DR is not a full-featured platform integration, very specifically it is a limited platform integration that attempts to normalize platform features for many platforms into a common set. This means it will never be a complete solution, it's not trying to be a complete solution.

{% hint style="warning" %}
Online Subsystem Steam and the related Steam Socket plugin from Epic Games for Unreal is very far out of date. Even if you wanted to keep to the Online Subsystem model. The Online Subsystem Steam is a liability you should be aware of.
{% endhint %}

In Unreal they have a standard approach to online systems e.g. friends, chat, sessions, etc. that is the "Epic" way to do things. They have created an "Online Subsystem" framework of many popular live operations/backend services such as "Online Subsystem Steam" ... as well as Facebook, Google, etc.

Online Subsystem Steam shoehorns the Steam API and tries to make it fit the Epic concept of an Online Subsystem.&#x20;

{% hint style="info" %}
This can be useful when you want to do a multi-platform game and have all the different builds have the same basic online features but use each platform (we don't recommend this).
{% endhint %}

{% hint style="danger" %}
It falls apart when you want to take full advantage of a platform's features and capabilities.
{% endhint %}

Epic Games does try to compensate for the limitations of Online Subsystem regarding Steam API with several add-on plugins such as Steam Controller however this doesn't address the fact that Online Subsystem Steam is very far out of date nor the limitations with some of Valve's most valuable features in Steam Lobby, Steam Game Server, Steam Workshop, Steam Inventory.

{% hint style="info" %}
For note, the "Heathen" way to handle multi-platform live operations (what Unreal calls an Online Subsystem) is to use a non-platform specific one ... such as PlayFab, GameLift, Photon, etc.

These are not platform-specific and work on all platforms, this will ensure that you are not limited to a knee-capped common feature set among all platforms but rather can fully exploit the robust features of a specific tool that is its self multi-plat and can be applied to any distribution platform.
{% endhint %}

### Steamworks.NET SteamManager.cs

This original came from an example of using the raw Steamworks.NET C# wrapper you can find the original at the link below

{% embed url="https://github.com/rlabrecque/Steamworks.NET-Example" %}

Keep in mind this was an example script, meant to be used with a specific example project and like any example script

{% hint style="danger" %}
Was never meant for production use
{% endhint %}

Sadly a great many Unity Asset developers do what Unity Asset developers often do and copy and paste someone else's work into their own asset and run with it without actually understanding what it was, why it was or how to do it properly.

{% hint style="info" %}
SteamManager should not be present much less used in any project. It's a learning tool, not production code.
{% endhint %}

The functionality that SteamManager provided in its original context is handled by Heathen's systems. We provide both a free lite version and a paid full-featured version [for Unity](../toolkit-for-steamworks-sdk/unity/).

## Getting Help

This Knowledge Base is your best source for information not just on Steam but all manner of Game Development tasks.

### Navigation

:eyes: Look to your left, that is the navigation panel and can be used to browse the Knowledge Base. Many articles have sub-articles so check the little > arrow to the right of an entry.

### AI Search and Classic Search

In the Upper right corner, you will find a search box&#x20;

<figure><img src="../.gitbook/assets/image (508).png" alt=""><figcaption></figcaption></figure>

That Search box has an AI function called Lens

<figure><img src="../.gitbook/assets/image (615).png" alt=""><figcaption></figcaption></figure>

Like any AI tool, it is a biased search so isn't perfect but it does link the articles it found with related information in the "Answer based on X sources" drop-down at the bottom left. It also of course has a standard search function.

### Discord

{% embed url="https://discord.gg/6X3xrRc" %}

Linked at the top of this knowledge base is a link to our Discord server where you can get live support from the wider community and Heathen developers. This is the best method for asking a question when you can't find the answer here in the Knowledge Base.

The Discord community is there to help you as a game developer so feel free to ask questions about any game development-related topic you might have. As to support for each of Heathen's assets, each has a dedicated channel for that.

### Direct Message

Once you join Discord you will be able to directly message the Heathen staff you see there ... they are denoted by the `| Heathen` at the end of their name. We do keep DMs to a minimum so if your question doesn't require a private conversation we will answer you in the appropriate server channel.&#x20;

Direct Message is not a means to get a faster response, it's a resource available when you need a bit more confidentiality than a public chat forum.

### Email

While not recommended as it's slow, error-prone, and all around the least effective of the available support options Heathen can be contacted for support at `heathen dot group` we will get back to you as soon as possible. Please be aware that emails may be trapped by spam, are an indirect method of communication, and will require an additional lead time to get back to you.
