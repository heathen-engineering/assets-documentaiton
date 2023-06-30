---
description: Have a question? Get an Answer!
---

# ⁉ F.A.Q

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Offline Documentation?

<figure><img src="../../.gitbook/assets/image (1) (7).png" alt=""><figcaption></figcaption></figure>

The code is fully commented and documented as a result you can use your IDE's "Object Explorer" to view all the objects in our asset, see all the members in each object and review the comments and notes on every field and attribute with in.

We do not provide PDF style documents for the asset.

## Unity or Godot?

Either, Heathen's Steamworks was originally created as a Unity asset however we have ported the free [Foundation ](https://github.com/heathen-engineering/SteamworksFoundation)version to Godot and are in the process of porting the Complete version.

### What Version?

Godot (mono) 3.5 or later. \
To keep the code base between the two engines as close as possible and thus maintenance costs and bugs in check we use C# thus you need the "mono" version of the engine.

Unity 2021 LTS or later\
As per Unity's request we maintain all Unity assets on the oldest in support Unity version at current that is 2021 LTS.&#x20;

> 2020 LTS was supported through the v2.x life cycle. Unity is expected to release 2022 LTS around the end of March or early April dropping 2020 LTS making 2021 LTS the "legacy" LTS\
> \
> We do not use engine features in our functional code but our editor extensions of course use engine features. In most cases you can "back port" Steamworks to Unity 2019 or later with little or no issue however we cannot support it beyond community guidance as Unity doesn't support versions older than the legacy LTS.

## Can this do \<X>

If X is something the Steam API can do then yes.\
That is to say we cover 100% of the Steam API by virtue of being built on top of Steamworks.NET and extending that fundamental Steam API wrapper as opposed to trying to replaces it (as Facepunch does). As a result, if you can do it with Valve's Steam API then you can do it with Heathen's Steamworks.

### Code free?

Simple features such as initializing Steam API, loading and handling stats, achievements and leaderboards and even basic uses of the user's data such as fetching the users name, avatar image, etc. can in fact be done code free right out of the box.

Our prefabs even enable you to do many common things such as listing Friends into groups, displaying a Leaderboards entries and even Party and Quick Match lobby systems all code free.

{% hint style="info" %}
Trying to do everything you can "Code Free" or with "Visual Scripting"?\
Read our article here on [Visual Scripting](../../company/development/visual-scripting.md) and maybe check out the rest of our Guides. Heathen is here to help you Do More and that means more than just selling you best in class Unity assets.
{% endhint %}

More complex features, and make no mistake Steam API is absolutely huge and has many many features some of which such as Steam Inventory can be incredibly complex ... these more complex features will \* **always** \* require you to "program" the logic that exploits them with respect to your game's needs. Depending on what tooling your using such as Bolt or other "visual scripting" tools you can still do it "Code Free" thanks to our tools and components layers.

### With the free version?

You can find a comparison of what is included in [Steamworks Foundation](./#feature-comparison) on the main page in this knowledge base.&#x20;

Keep in mind you can get instant access and a license to keep forever of Steamworks Complete ... and every other major Heathen asset for $15 by becoming a [GitHub Sponsor](../../become-a-sponsor/) and yes you can cancel any time and keep what you downloaded and the license to use it.

### What about Microtransactions / Cash Shop?

Yes of course, Steam API handles MTX (micro transactions) via the Steam Inventory interface. Heathen's Steamworks Complete has robust tooling around [Steam Inventory](../../company/steam/steamworks/inventory/) which can greatly help any developer regardless of skill set.

> To reiterate as its often hard to believe, yes Steam API does MTX, yes it is [Steam Inventory](../../company/steam/steamworks/inventory/) that is used to do that.

## Can I try before I buy?

Yes its called [Steamworks Foundation](https://github.com/heathen-engineering/SteamworksFoundation) and is free to use. It has a limited feature set but is the same code used in the "full fat" Complete version.&#x20;

When ready you can get instant access and a license to keep forever of Steamworks Complete ... and every other major Heathen asset for $15 by becoming a [GitHub Sponsor](../../become-a-sponsor/) and yes you can cancel any time and keep what you downloaded and the license to use it.

## Can I use this for commercial games?

Of course, have a look at some of the [great games that already use this](https://store.steampowered.com/curator/42461073-Made-with-Heathen).

<figure><img src="../../.gitbook/assets/Made with Heathen.jpg" alt=""><figcaption><p>Made with Heathen Steam Curator lists a few of the games published on Steam that are made with Heathen technology including but not limited to Heathen's Steamworks.</p></figcaption></figure>

{% embed url="https://store.steampowered.com/curator/42461073-Made-with-Heathen" %}
Some of the games that have been Made with Heathen technology.
{% endembed %}

## Does this work with X

1st off most tools such as UMA, Character Controllers, etc. do not impact Steam API at all and are not impacted by Steam API at all. So in most cases rather or not you use Steam API has nothing to do with compatibility with those tools.

For tools that do integrate with Steam API the relevant information is; Heathen builds on top of Steamworks.NET so anything that makes \*\***Proper**\*\* use of Steamworks.NET will simply work right out of the box.

How do you know its proper use?

1. Does not embed a copy of Steamworks.NET in its source code. Steamworks.NET should always be installed fresh from GitHub preferably via the Unity Package Manager as described on our [installation page](broken-reference).
2. Does not make \*\***ANY**\*\* use of SteamManager.cs\
   SteamManager.cs is an example script originally authored by the same developer that authors Steamworks.NET ... you can find its original form [here](https://github.com/rlabrecque/Steamworks.NET-Example). It is meant to be a demonstration of how a programmer would initialize the Steam API ... it is absolutely not meant to be production code. Sadly many samples, examples and even some "assets" are had coded to use it.

### Any Given Networking Tool?

1st yes, the networking tool you choose to use wont impact Steam API at all. Rather or not Steam API impacts it depends on rather or not that networking tool uses Steam Networking Interfaces. If it does then it needs to make proper use Steamworks.NET ... which is a low bar to meet.

This is not something for us or Steamworks.NET to do its something for the networking tool in question to do. The following tools are known to have working proper integrations with Steamworks.NET or to not use Steam Networking at all.

### Fish Networking?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

### Mirage?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

### Mirror?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

### NetCode for GameObjects?

Yes: You can find more information in the [Networking Integrations](unity/installation/networking-integrations.md) article.

### Photon (any variation)?

Yes: Photon is its own platform, uses its own networking interfaces and has no impact on nor is it impacted by Steam API in any way that comes to mind.

### SpatialOS?

Yes: SpatialOS is its own platform, uses its own networking interfaces and has no impact on nor is it impacted by Steam API in any way that comes to mind.

## Updates?

### GitHub Sponsors

GitHub Sponsors have access to the "Source Repo" this is the place where we do the actual work so updates are frequent and instant as we make them. It is GitHub so you can of course review every single update, each check-in, every comment ... full tracked and managed version history.

### Unity Asset Store

Unity Asset Store is updated each quarter (every 3 months) with the consolidated changes made in GitHub Source Repo.

In the event of a critical issue such as Steam, Unity, etc. making a breaking change to the API or engine we will update Unity Asset Store as quickly as possible and can offer ad-hoc patches via our Discord community.

### Major Updates

We release major updates every 2 to 3 years, GitHub Sponsors see these as any other update as they are working on the source directly.

Unity Asset Store users will see this as a paid major update. As typical with major updates on Unity Asset Store users that have purchased recently (with the last 90 days) will receive the update for free, all other users will receive a decaying discount.

#### What is a decaying discount?

The discount starts out steep as much as 80-90% off the base price. As the update ages the discount reduces to 0 over the course of 2 years. That is after 2 years past the release of a major update you will be paying the "sticker price".
