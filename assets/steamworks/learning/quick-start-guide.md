---
description: A quick start guide for those already comfortable with the basics.
---

# Quick Start Guide

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Steam Settings

Create a new Steam Settings object in your project folder by right clicking in your project tab and selecting\
**Create > Steamworks > Settings**

![](<../../../.gitbook/assets/image (158) (1) (1) (1) (1).png>)

## App Id

Enter your app ID in the Application Id field**.**  If you don't have an application ID just yet that's fine you can work with the test App ID 480 however there will be some limitations.&#x20;

{% hint style="info" %}
You obviously cannot deploy your app without an App ID

You cannot create your own achievements, stats or other artifacts without your own ID



Valve issues you an App ID when you pay your application fee. If you don't have your own ID yet you can use App ID 480 as a test ID. Heathen's samples and demos all use App ID 480.
{% endhint %}

## Steamworks Behavior

Create a [Steamworks Behaviour](broken-reference) object in your [bootstrap scene](../../../company/concepts/bootstrap-scene.md) or similarly appropriate location; and drag your Steam Settings object into the provided field.

![](<../../../.gitbook/assets/image (161) (1) (1) (1) (1) (1) (1).png>)

Congratulations, you are now integrated with the Steam APIs. If you run the simulation, you will see that the Steam API initializes and is ready for use.

{% hint style="danger" %}
[Steamworks Behaviour](../components/steamworks-behaviour.md) should be initialized early in your application and never destroyed. It is keenly important that you do not reload the scene that defines the [Steamworks Behaviour](../components/steamworks-behaviour.md) as this will cause issues with the Steam API.



If you need to reload the scene where [Steamworks Behaviour](../components/steamworks-behaviour.md) is located or otherwise must use a single scene architecture you should use the [Steamworks Creator](../components/steamworks-creator.md) to insure the Steam API is managed correctly.
{% endhint %}

## Networking

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/developer-articles/multiplayer-steam-games" %}
This is a good place to start when learning about Steam and multiplayer games
{% endembed %}

{% hint style="success" %}
Steamworks Complete and whatever HLAPI you chose to work with have no impact on each other at all. You will use Steamworks and your HLAPI of choice exactly the same with as you would without the other.
{% endhint %}

### Do I need Steamworks Complete?

You do not "require" Steamworks Complete in order to use Mirror, FishNetworking or NetCode for GameObject's or any other Steam transports. Those transports like our self work with Steamworks.NET directly.

That said you will need to initialize, configure and manage the Steam API before SteamNetworking interfaces can be used. Our Steamworks Complete and Steamworks Foundation packages make working with Steam API simple and stable. If you do not use Steamworks Complete or Foundation you would need to use the raw Steam API to initialize and configure your Steam API integration your self before your HLAPI could use the Steam transports.

### Examples?

Where can I find examples on using Steamworks Complete and (the HLAPI I chose)?

You cant because their is no need. Both Steamworks Complete and your HLAPI of choice work exactly the same rather or not the other exists. Thus we do not have an example of using (your HLAPI of choice) along side our Steamworks Complete.&#x20;

If you want to see an example of using your HLAPI of choice with your HLAPI's Steam transport then you should contact them. We have links to [Fish Networking, Mirror and NetCode for GameObjects in our articles](../installation/networking-integrations.md) but any HLAPI that works with Steamworks.NET properly will work.

If your looking for examples on how to initialize, configure and use Steam API (in general) you will find various samples in the provided [samples scenes](../../physkit/learning/sample-scenes/) and examples throughout our knowledge base.

If your trying to wrap your head around creating a [multiplayer game on the Steam platform](developer-articles/multiplayer-steam-games.md), we have an article for that as well. That article is not specific to any given HLAPI because the HLAPI you choose has no impact on the concepts involved.
