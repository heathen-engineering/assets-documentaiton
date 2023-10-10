---
description: Taking your very first step!
---

# ☝ Quick Start

{% hint style="success" %}
#### Like what you're seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools, and assets, escalated support and issue tracking, and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
### Working in Unreal, Unity or Godot?

We author the top [Steam Integration](../../heathens-steamworks-complete/steamworks.md) for Unity & are porting to Godot!

[Learn More!](../../heathens-steamworks-complete/steamworks.md)
{% endhint %}

Your first step is to navigate to [partner.steamworks.com](https://partner.steamgames.com/) we strongly recommend you create a new Steam account to represent you as a publisher or developer separate from any personal account/s you might have. Remember, new Steam accounts start as "limited" put $5 in your Steam wallet to get around this.&#x20;

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

You can test some features of Steam API using the test application "Spacewars" whose app Id is 480. This is the app id we use in all of our [Steamworks](../../heathens-steamworks-complete/steamworks.md) sample scenes and doesn't require you to even be signed up to use it.

Having said that you can't do anything meaningful with the test app, it exists as a teaching tool. To create the stats, achievements, leaderboard, workshop, etc. for your game you will require an App ID and we do recommend you do this as soon as you are sure you want to release your game on Steam ... no reason to wait.

## Steam API

Once you're all set up as a Steam Developer and have your App ID your next step should be to get familiar with the Steam API and what it has to offer. Heathen creates the best Steam integration for Unreal, Unity and Godot, read more on our [Steamworks page](../../heathens-steamworks-complete/steamworks.md).

Steam API is a tremendous value especially for small and indie developers as it is a power set of backend services and is completely free for you to use. We strongly recommend you understand what Steam API can do for your game before you commit your design. The best and most successful games fully exploit Steam's features.

## Installing Heathen's Steamworks

Now that you have made the wise decision to use Heathen's Steamworks to integrate Steam API with your game project on [Unreal](../../heathens-steamworks-complete/unreal/installation.md), [Unity](../../heathens-steamworks-complete/unity/installation/) or [Godot ](../../heathens-steamworks-complete/godot/installation.md)you will need to get it installed and configured for use!

[Install Heathen's Steamworks for Unreal](../../heathens-steamworks-complete/unreal/installation.md)

[Install Heathen's Steamworks for Unity](../../heathens-steamworks-complete/unity/installation/)

[Install Heathen's Steamworks for Godot](../../heathens-steamworks-complete/godot/installation.md)

## Unlearning Bad Habits

Unfortunately, there is a lot of just horrible sample and example code out there, especially around Steamworks / Steam API for Unity. Here are some common things you might have picked up or learned that you should throw out right now.

### SteamManager.cs

This original came from an example of using the raw Steamworks.NET C# wrapper you can find the original at the link below

{% embed url="https://github.com/rlabrecque/Steamworks.NET-Example" %}

Keep in mind this was an example script, meant to be used with a specific example project and like any example script

{% hint style="danger" %}
Was never meant for production use
{% endhint %}

Sadly a great many Unity Asset developers do what Unity Asset developers often do and copy and paste someone else's work into their own asset and run with it without actually understanding what it was, why it was or how to do it properly.

{% hint style="info" %}
SteamManager should not be present much less used in any project
{% endhint %}

The functionality that SteamManager provided in its original context is handled by Heathen's systems. Please see the [Steamworks Behaviour](../../heathens-steamworks-complete/unity/components/steamworks-behaviour.md) for a similar but quite different approach.

## Getting Help

This Knowledge Base is your best source for information not just on Steam but all manner of Game Development tasks.

### Navigation

:eyes: Look to your left, that is the navigation panel and can be used to browse the Knowledge Base. Many articles have sub-articles so check the little > arrow to the right of an entry.

### AI Search and Classic Search

In the Upper right corner, you will find a search box&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

That Search box has an AI function called Lens

<figure><img src="../../.gitbook/assets/image (24) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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
