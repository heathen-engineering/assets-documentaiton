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

![](<../../../.gitbook/assets/image (158) (1).png>)

## App Id

Enter your app ID in the Application Id field**.**  If you don't have an application ID just yet that's fine you can work with the test App ID 480 however there will be some limitations.&#x20;

{% hint style="info" %}
You obviously cannot deploy your app without an App ID

You cannot create your own achievements, stats or other artifacts without your own ID



Valve issues you an App ID when you pay your application fee. If you don't have your own ID yet you can use App ID 480 as a test ID. Heathen's samples and demos all use App ID 480.
{% endhint %}

## Steamworks Behavior

Create a [Steamworks Behaviour](broken-reference) object in your [bootstrap scene](../../../company/concepts/bootstrap-scene.md) or similarly appropriate location; and drag your Steam Settings object into the provided field.

![](<../../../.gitbook/assets/image (161) (1) (1) (1).png>)

Congratulations, you are now integrated with the Steam APIs. If you run the simulation, you will see that the Steam API initializes and is ready for use.

{% hint style="danger" %}
[Steamworks Behaviour](../components/steamworks-behaviour.md) should be initialized early in your application and never destroyed. It is keenly important that you do not reload the scene that defines the [Steamworks Behaviour](../components/steamworks-behaviour.md) as this will cause issues with the Steam API.



If you need to reload the scene where [Steamworks Behaviour](../components/steamworks-behaviour.md) is located or otherwise must use a single scene architecture you should use the [Steamworks Creator](../components/steamworks-creator.md) to insure the Steam API is managed correctly.
{% endhint %}

##
