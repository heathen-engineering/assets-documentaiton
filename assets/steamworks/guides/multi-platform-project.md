---
description: Managing a multi-platform build
---

# Multi-Platform Project

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article will go over the considerations, problems and available solutions when building for multi-platform.

{% hint style="warning" %}
No it is not possible to truly have 1 code base for all platforms.\
\
While many would like to say it is, what they are really referring to is conditional compilation where in compiler adds or removes code from the build based on script defines / build target.\
\
This however means that in Unity Editor the code is very different from what will be compiled causing many issues in development and testing.
{% endhint %}

The first and most important thing is to understand that Steamworks.NET the core dependency for Steam API integration will \*\***NOT**\*\* compile for any platform other than

* Mac (client or server)
* Linux (client or server)
* Windows 32 or 64 bit (client or server)

This means that it will not compile for&#x20;

* Android
* iOS
* Windows Universal
* Web GL
* XBox
* PlayStation
* Switch

or any other built target you might select.

## Built Target

Because Steamworks.NET simply will not compile or be available at all in editor or otherwise for any built target other than the three listed

* Mac (client or server)
* Linux (client or server)
* Windows 32 or 64 bit (client or server)

Then switching your project to any built target other than those will result in compiler errors.

You can make the compiler errors go away by adding the script define `DISABLESTEAMWORKS` to the Player settings Script defines .... however you should never do this in the Editor.

Why not in the editor?

Because if you do this Unity will not compile any of the Steam related scripts thus any use of those scripts in a scene or GameObject will be removed the next time Unity saves thus breaking all references to all Steam related scripts and objects.

That is if you for example set your editor to `Android` and applied the `DISABLESTEAMWORKS` define to tell the compiler to not compile Steamworks Complete or Steamworks Foundation then Unity will see that those scripts no longer exist, it will then remove them from the GameObject on the next save.

## Solution: Build Service

For this you will need to keep your Editor always set to a valid Steam build target such as&#x20;

* Mac (client or server)
* Linux (client or server)
* Windows 32 or 64 (client or server)

This is to insure that the Unity Editor does not strip out any of the code that you need to work with and does not break references to any of the objects you need to work with.

In order to test other platforms you will need to use a build service, there are many to choose from and we have listed a few in the Build Service article found here. You will configure your build targets for each platform and for any platform that should not use Steam you will add the `DISABLESTEAMWORKS` script define.

## Solution: Multi-Project

This is simply having 1 Unity project for each target such as&#x20;

* Steam
* Itch
* Mobile
* Console
* etc.

For any project of any level of complexity this is likely how you will need to go rather or not your using Steam. Why? if your fully exploiting the features of a platform and intend to test them in Editor you will need your UI, logic and other features to adjust per-target. You can do this to some extent with [conditional compilation](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html) however that is limited especially when dealing with platforms that are on the same Unity build type such as Steam, Itch, etc.

Also if your building optimally you will want to strip your build down to only that which is required ... this is especially true for platforms sensitive to build size so mobile and web in particular. To do this you want to make sure your not including assemblies that aren't being used, e.g. even if you could you wouldn't want to include Steamworks.NET in a Mobile build ... fortunately you cannot it strips its self, but it would not strip from say an Itch.io build even though you wont be using it there.
