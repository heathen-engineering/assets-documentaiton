---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
---

# Online Subsystem

## Introduction

{% hint style="success" %}
Online Subsystem is not required to do Multiplayer in Unreal\
\
The Online Subsystem framework is simply a means of abstracting backend services to a "common" form e.g. a subsystem. In most use cases this is completely undesired, if you are building a Steam game then you want to fully utilize the Steam API not just the subset of features common to all similar systems.\
\
If you do want a multiplatform system then you would be far better off using a multiplatform service such as PlatFab or GameLift as opposed to trying to dumb down all other systems to some common set.
{% endhint %}

An Unreal Online Subsystem is a framework that attempts to normalize the use of typical backend systems to a standard or common form. In theory, this would mean you could code to the Online Subsystem standard and interchangeably swap in and out various systems such as Facebook, Steam and EGS.

{% hint style="info" %}
The limitations of Online Subsystem as a framework are common reasons why developers would choose to use Heathen's Toolkit for Steamworks.

\
While the Online Subsystem framework is limiting if there is a demand for it we can create an Online Subsystem wrapper. Join our discord and let us know what you want!
{% endhint %}

## Considerations

In practice, however, there is more to all of these systems than the Online Subsystem can leverage and these systems can not be fully normalized. If you wanted to create a multiplatform game that had the same features and functionality across all systems then you should use a multiplatform system such as

* GameLift (Amazon)
* PlayFab (Microsoft)

PlayFab and GameLift are by far the largest and most capable options for multiplatform live service-like games however there are other smaller options such as.

* Facebook
* Machinations
* Epic Game Services
* Unity Game Services
* AppLovin
* G Portal
* etc.

The Online Subsystem framework for multiplatform is thus highly limiting, if you not trying to create a multiplatform game then the platform APIs of the platform you choose are generally easier to use and far more robust than an Online Subsystem can account for. As you won't be switching between more than one there is no reason to not use the platform API directly.

* Steam
* GoG&#x20;
* Facebook
* Google
* Apple
* PlayStation
* Xbox

In all cases, these platforms are platforms and not simply "Live Ops" solutions. They work more like and in some cases outright are social networks including rich social features that are specific to each platform and thus can't be normalized by a common framework in a meaningful way.

## Alternative

Steam API doesn't have to have any impact on your multiplayer set-up or management of sessions. The API offers inventory services, leaderboards, stats, achievements and many other features that are not limited to networking or multiplayer topics.

For multiplayer games, an Online Subsystem is not required. It is the configured Net Driver that handles the network transport. Heathen has developed a [Sockets Net Driver](sockets-net-driver.md) that is not dependent on an Online Subsystem that leverages Steam Networking Sockets find more [here](sockets-net-driver.md). Unreal's synchronization handles syncing data. The Online Subsystem is primarily a means to find and advertise "sessions".

Platforms such as Steam have their own mechanisms to create, find and share sessions of various types and Heathen provides you with the tools to use those features. See our [Multiplayer ](../../company/steam/steamworks/multiplayer/)articles for more information on the tools, systems and concepts at play with Multiplayer games on Steam.
