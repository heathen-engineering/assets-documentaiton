---
description: Have a question? Get an Answer!
cover: ../.gitbook/assets/Banner.jpg
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

# F.A.Q

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Offline Documentation?

<figure><img src="../.gitbook/assets/image (1) (7).png" alt=""><figcaption></figcaption></figure>

The code is fully commented and documented as a result you can use your IDE's "Object Explorer" and [IntelliSense ](../company/development/intellisense.md)features to view all the objects in our asset, see all the members in each object and review the comments and notes on every field and attribute within.

We do not provide PDF-style documents for the asset. Your IDE's Object Explorer, Your IDE's [IntelliSense](../company/development/intellisense.md) and this Knowledge Base and its AI-driven search tools should prove a superior option to any static file-based documentation. If you have any questions please reach out to us on our [Discord](https://discord.gg/eVVgM36).

## Engine

### Godot

Currently Heathen's Toolkit for Steamworks is available as a lite "Foundation" package containing the core systems as a proof of concept for Gotdot C# 3.5 We are monitoring the engine development and community need and will port Steamworks Toolkit to Godot C# as the platform stabilises or as demand calls for it. If you need Steamworks Toolkit on Godot reach out and let us know.

### Unity

Heathen's Toolkit for Steamworks comes in a full "Complete" and a lite "Foundation" package for Unity through GitHub Sponsor and the Unity Asset Store.

### Unreal

Heathen's Toolkit for Steamworks is available for Unreal through GitHub Sponsor and the Unreal Marketplace.

## Can this do \<X>

If X is something the Steam API can do then yes.\
For Unity and Godot we build on Steamworks.NET and for Unreal we integrate the full native Steam API.&#x20;

Our design is thus built on top of the native Steamworks SDK in layers of abstraction that allow us to&#x20;

* Deliver simple tools for ease of use
* Provide boilerplate systems saving you huge amounts of time
* Built on native foundation, if Steam can do it at all you can do it with Heathen's Steamworks&#x20;

### Code free?

Short answer, yes

In Unreal we have exposed the entire SDK to blueprints with additional widgets and tools built on top to further simplify the process.

In Unity we have created Managers and components that handle most common tasks with simple configuration and of course, our tools are compatible with most visual scripting tools.

For all engines, we have built additional systems, templates and ready-to-use components to handle common use cases and take care of all the boiler plate for you.

Simple features such as initializing Steam API, loading and handling stats, achievements and leaderboards and even basic uses of the user's data such as fetching the users name, avatar image, etc. can in fact be done code-free right out of the box.

For Unity our prefabs even enable you to do many common things such as listing Friends into groups, displaying Leaderboards entries and even Party and Quick Match lobby systems all code-free.

### What about Microtransactions / Cash Shops?

Yes of course, Steam API handles MTX (microtransactions) via the Steam Inventory interface. Heathen's Toolkit for Steamworks has robust tooling around [Steam Inventory](../company/steam/steamworks/inventory/) which can greatly help any developer regardless of skill set.

> To reiterate as its often hard to believe, yes Steam API does MTX, yes it is [Steam Inventory](../company/steam/steamworks/inventory/) that is used to do that.

## Can I try before I buy?

For Unity, Yes it's called [Steamworks Foundation](https://github.com/heathen-engineering/SteamworksFoundation) and is free to use. It has a limited feature set and isn't able tobe updated to the latest all the time but is the same code style used in the "full fat" complete version.&#x20;

For Unreal, we are working on an equivalent to "Foundation" but don't have anything to announce at this time.

## Can I use this for commercial games?

Of course, have a look at some of the [great games that already use this](https://store.steampowered.com/curator/42461073-Made-with-Heathen).

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://store.steampowered.com/curator/42461073-Made-with-Heathen" %}
Some of the games that have been Made with Heathen technology.
{% endembed %}

## Does this work with \<name of other tool>?

1st off most tools such as UMA, Character Controllers, etc. do not impact Steamworks at all and are not impacted by Steamworks at all. So in most cases whether or not you use Steamworks has nothing to do with compatibility with those tools.

For tools that do integrate with Steamworks&#x20;

### Unreal

For Unreal, anything working with the native SteamShared plugin (Unreal's built-in integration) should be fine.

### Unity

For Unity, the relevant information is; that Heathen builds on top of Steamworks.NET so anything that makes \*\***Proper**\*\* use of Steamworks.NET will simply work right out of the box.

Sadly Unity Assets seen on the Asset Store rarely make proper use of Steamworks.NET and very often, very wrongly copy the full Steamworks.NET source into the project root causing a myriad of issues rather or not you use our kit.

We do work with Unity Asset developers such as Mirror, FishNetworking and even the NetCode for GameObjects community to help them make proper use of Steamworks.NET and in those cases, you will have no issues.

How do you know its proper use?

1. Does **NOT** embed a copy of Steamworks.NET in its source code. Steamworks.NET should always be installed fresh from GitHub preferably via the Unity Package Manager
2. Does not make \*\***ANY**\*\* use of SteamManager.cs\
   SteamManager.cs is an example script originally authored by the same developer that authors Steamworks.NET ... you can find its original form [here](https://github.com/rlabrecque/Steamworks.NET-Example). It is meant to be a demonstration of how a programmer would initialize the Steam API ... it is absolutely not meant to be production code. Sadly many samples, examples and even some "assets" are hard coded to use it.

## How does networking work?

### Unreal

For Unreal everything is box standard. You can either use Open Level directly (our preference) or you can use tools like Advanced Sessions. Our Example level is fully functional and can be used to test multiplayer including detailed Blueprint implementation in the example UI.

### Unity

1st yes, the networking tool you choose to use won't impact Steamworks at all. Whether or not Steamworks impacts it depends on whether or not that networking tool uses Steam Networking Sockets. If it does then it needs to make proper use Steamworks.NET ... which is a low bar to meet and most reputable solutions do.

This is not something for us or Steamworks.NET to do it is something for the networking tool in question to do. The following tools are known to have working proper integrations with Steamworks.NET or to not use Steam Networking at all.

#### Fish Networking?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

#### Mirage?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

#### Mirror?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

#### NetCode for GameObjects?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

#### Photon (any variation)?

Yes: Photon is its own platform, uses its own networking interfaces and has no impact on nor is it impacted by Steam API in any way that comes to mind.

## How do Asset Updates work?

### [GitHub Sponsors](../where-to-buy/become-a-sponsor.md)

GitHub Sponsors have access to the "Source Repo" This is the place where we do the actual work so updates are frequent and instant as we make them. It is GitHub so you can of course review every single update, each check-in, and every comment ... fully tracked and managed version history.

### Asset Stores ([Unreal ](https://www.unrealengine.com/marketplace/en-US/product/steam-api-steamworks-complete)or [Unity](https://assetstore.unity.com/packages/tools/integration/steam-api-steamworks-complete-246652))

Unity Asset Store and Unreal Marketplace are updated each quarter (every 3 months) with the consolidated changes made in GitHub Source Repo if relevant or more frequently in the case of a critical issue.

In the event of a critical issue such as Steam, Unity, etc. making a breaking change to the API or engine, we will update the stores as quickly as possible and can offer ad-hoc patches via our Discord community.

## How do Paid Updates work?

### [GitHub Sponsors](../where-to-buy/become-a-sponsor.md)

Not relevant, as you working on our Source Repository you have instant access to our changes as they happen thus there is no "upgrade path" needed you will naturally have access to the next version as it develops.

### Asset Store / Marketplace / FAB

We have an article dedicated to the [Maintenance Cycle](maintenance-cycle.md) which defines this. In short, a new version will released yearly and you get an 80% discount on it to continue receiving that year's updates. The old version keeps working, we don't remove access, your license is perpetual this is simply paying for the next year's worth of updates and support.

## From one store can I get access to the other?

{% hint style="info" %}
FAB offers both a Unity and Unreal version
{% endhint %}

In short no.

Each store is its own walled garden operated by that platform (Epic's Unreal Marketplace, Unity's Unity Asset Store). They define the terms of the license, they handle payment processing and refunds. Everything about the relationship is actually with them. We won't even know you exist unless you introduce yourself to us.

We cannot grant you access to an asset on either store for any reason but we especially wouldn't be permitted to grant you a license on Unreal from Unity Asset Store or vice versa ... they are competitors.

If you want access to our asset for any engine then you want[ GitHub Sponsor](../where-to-buy/become-a-sponsor.md).\
GitHub Sponsors (or Patreon) have access to all of our assets for all engines, including tools and code that we do not publish on the asset stores. We control the license terms in that case and we do so via a [Site Based license](../where-to-buy/heathen-license-agreement.md).&#x20;

## From a store can I get access to GitHub?

By sponsoring for $15 or more yes,

If you asking if we can transfer your Unity Asset Store or Unreal Marketplace license to GitHub Sponsor or Patreon membership then no I am afraid not.

Unity has hinted they may introduce such a feature but at current Unity Asset Store and Unreal Marketplace are walled gardens. We cannot transfer licenses in or out of either, we cannot grant you access to one from the other and we certainly wouldn't be allowed to convert you to a direct customer through there interface they want to keep you in their garden :smile:
