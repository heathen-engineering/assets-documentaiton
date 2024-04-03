---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
---

# Updating Steamworks SDK

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
You almost certainly do not need to update Steamworks SDK.\
\
If you decide you do understand you will need to build the engine from source.\
\
Building the engine from the source is not as scary as it sounds and is required if you plan on building a Dedicated server anyway.
{% endhint %}

This article will help you update the built-in Steamworks SDK version and highlight all the requirements. This assumes you are building the engine from the source as the note above indicates.

### Do I need to update?

In most cases, no

Valve's Steamworks SDK doesn't stop working just because there is a new version, for obvious reasons, the main one being that it would cause every prior game to break. Most of the time when Valve makes a change to Steamworks APIs it is on the back end and doesn't impact the SDK. There are a few occasions where they have updated the SDK its self but in most of those, its adds quality-of-life features like the steam\_flat structure which simply makes including steam in your source easier in particularly for non-C-based projects.

There are a few points where Valve will add features such as May 2023 when they added identity to the Steam Authentication system. This change doesn't invalidate prior versions so you can keep using whatever version prior to that without issue however if you want to leverage the new identity field you will need to update your built version of Steamworks SDK

## Source Access

Because we will be making a change to the Unreal Engine its self we do need the ability to rebuild it. To do this you will need GitHub access to Unreals source. You cannot rebuild the engine from the Launch Download version, even if you have the Source at least not at the time of this writing.

To get source access to Unreal Engine code follow the instructions documented here.

{% embed url="https://www.unrealengine.com/en-US/ue-on-github" %}

Once that is complete you will need to clone a copy of the code, we recommend you make a fork and name it for the version of the engine and for whatever change you are doing for example.

`UnrealEngine-5.3-Steamworks-1.59`

The Unreal Engine's source is huge and will take a very long time to clone compared to most repositories you have likely worked with.

## Steamworks Version

Make sure you have your Developer account as you will need that first ... we have an article on getting started here.

Once you have that download the desired version of Steamworks SDK

{% embed url="https://partner.steamgames.com/downloads/list" %}

{% hint style="info" %}
Our general advice is to only update as far as you require for whatever feature it is you are after. For example, if you want the new identify field in Unreal 5.3 ... you could update to Unreal 5.4 where they do that for you, or you can update to Steamworks 1.57 which is where it was introduced.\
\
Jumping further than that increases the chance you need to modify more engine code to get it to compile.
{% endhint %}

## Modify the Engine

Next, we need to update the Steamworks ThirdPartyPlugin to use the newly downloaded version. There are instructions for that here.

{% embed url="https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine#downloadingsteamworks" %}

In short, you're going to copy the `sdk/public` and `sdk/redistributable_bin` folders into a folder named for the SDK version

<figure><img src="../../.gitbook/assets/image (413).png" alt=""><figcaption></figcaption></figure>

Next you will need to update the steamworks.build.cs to reference the new version

<figure><img src="../../.gitbook/assets/image (414).png" alt=""><figcaption></figcaption></figure>

You have 1 more spot to update in Heathen's Toolkit for Steamworks. Find our plugin and modify its ToolkitSteamworks.Build.cs for the specific version you're using.

{% hint style="info" %}
If you are running our plugin as an Engine plugin such as installed from the Unreal Marketplace then you will need to do this as part of the engine modification.

\
If you are running our plugin as a Project plugin e.g. as part of your game project's source you can compile the engine now and modify the plugin in your game project.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (415).png" alt=""><figcaption></figcaption></figure>

We use these defines to add and remove code at compile time enabling our plugin to work with any version of Steamworks from a single codebase. If a new version comes out that is not supported simply let us know in Discord or via a GitHub Issue and we will get that patched.

Recompile and everything should now be working on the version of Steamworks SDK you chose.
