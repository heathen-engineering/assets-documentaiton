---
description: Have a question? Get an Answer!
cover: ../.gitbook/assets/Banner@8x-100.jpg
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

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Offline Documentation?

<figure><img src="../.gitbook/assets/image (1) (7).png" alt=""><figcaption></figcaption></figure>

The code is fully commented and documented as a result you can use your IDE's "Object Explorer" and [IntelliSense ](../company/development/intellisense.md)features to view all the objects in our asset, see all the members in each object and review the comments and notes on every field and attribute within.

We do not provide PDF-style documents for the asset. Your IDE's Object Explorer, Your IDE's [IntelliSense](../company/development/intellisense.md) and this Knowledge Base and its AI-driven search tools should prove a superior option to any static file-based documentation. If you have any questions please reach out to us on our [Discord](https://discord.gg/eVVgM36).

## Engine

### Godot

At current Steamworks Foundation is available as a proof of concept for Gotdot C# 3.5 We are monitoring the engine development and community need and will port Steamworks Complete to Godot C# as the platform stabilises or as demand calls for it. If you have a need for Steamworks Complete on Godot reach out and let us know.

### Unity

Heathen's Steamworks Complete and Foundation are available for Unity through GitHub Sponsor and the Unity Asset Store.

### Unreal

Heathen's Steamworks Complete is available for Unreal through GitHub Sponsor. We intend to make the asset available on Unreal Marketplace soon.

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

### What about Microtransactions / Cash Shop?

Yes of course, Steam API handles MTX (microtransactions) via the Steam Inventory interface. Heathen's Steamworks Complete has robust tooling around [Steam Inventory](../company/steam/steamworks/inventory/) which can greatly help any developer regardless of skill set.

> To reiterate as its often hard to believe, yes Steam API does MTX, yes it is [Steam Inventory](../company/steam/steamworks/inventory/) that is used to do that.

## Can I try before I buy?

Yes it's called [Steamworks Foundation](https://github.com/heathen-engineering/SteamworksFoundation) and is free to use. It has a limited feature set but is the same code used in the "full fat" Complete version.&#x20;

When ready you can get instant access and a license to keep forever Steamworks Complete ... and every other major Heathen asset for $15 by becoming a [GitHub Sponsor](../become-a-sponsor/) and yes you can cancel any time and keep what you downloaded and the license to use it.

## Can I use this for commercial games?

Of course, have a look at some of the [great games that already use this](https://store.steampowered.com/curator/42461073-Made-with-Heathen).

<figure><img src="../.gitbook/assets/Made with Heathen.jpg" alt=""><figcaption><p>Made with Heathen Steam Curator lists a few of the games published on Steam that are made with Heathen technology including but not limited to Heathen's Steamworks.</p></figcaption></figure>

{% embed url="https://store.steampowered.com/curator/42461073-Made-with-Heathen" %}
Some of the games that have been Made with Heathen technology.
{% endembed %}

## Does this work with X

1st off most tools such as UMA, Character Controllers, etc. do not impact Steam API at all and are not impacted by Steam API at all. So in most cases whether or not you use Steam API has nothing to do with compatibility with those tools.

For tools that do integrate with Steam API the relevant information is; Heathen builds on top of Steamworks.NET so anything that makes \*\***Proper**\*\* use of Steamworks.NET will simply work right out of the box.

How do you know its proper use?

1. Does not embed a copy of Steamworks.NET in its source code. Steamworks.NET should always be installed fresh from GitHub preferably via the Unity Package Manager as described on our [installation page](broken-reference).
2. Does not make \*\***ANY**\*\* use of SteamManager.cs\
   SteamManager.cs is an example script originally authored by the same developer that authors Steamworks.NET ... you can find its original form [here](https://github.com/rlabrecque/Steamworks.NET-Example). It is meant to be a demonstration of how a programmer would initialize the Steam API ... it is absolutely not meant to be production code. Sadly many samples, examples and even some "assets" are had coded to use it.

### Any Given Networking Tool?

### Unreal

Yes, you can use our asset with the Steam Networking Sockets Plugin to work with Steam Networking via Unreal's multiplayer tools. Or you can of course go with EOS or other networking solutions.&#x20;

### Unity

1st yes, the networking tool you choose to use won't impact Steam API at all. Whether or not Steam API impacts it depends on whether or not that networking tool uses Steam Networking Interfaces. If it does then it needs to make proper use Steamworks.NET ... which is a low bar to meet.

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

#### SpatialOS?

Yes: SpatialOS is its own platform, uses its own networking interfaces and has no impact on nor is it impacted by Steam API in any way that comes to mind.

## Updates?

### GitHub Sponsors

GitHub Sponsors have access to the "Source Repo" this is the place where we do the actual work so updates are frequent and instant as we make them. It is GitHub so you can of course review every single update, each check-in, every comment ... full tracked and managed version history.

### Unity Asset Store

Unity Asset Store is updated each quarter (every 3 months) with the consolidated changes made in GitHub Source Repo.

In the event of a critical issue such as Steam, Unity, etc. making a breaking change to the API or engine, we will update the Unity Asset Store as quickly as possible and can offer ad-hoc patches via our Discord community.

### Unreal Marketplace

Coming soon, we will be shipping Steamworks Complete on the Unreal Marketplace in the future. At the moment we are in a stage of rapid development of the Unreal Steamworks Complete plugin so it's only available to GitHub Sponsors during this phase.&#x20;

### Major Updates

We release major updates every 2 to 3 years, GitHub Sponsors see these as any other update as they are working on the source directly.

Unity Asset Store users will see this as a paid major update. As typical with major updates on Unity Asset Store users who have purchased recently (within the last 90 days) will receive the update for free, and all other users will receive a discount.
