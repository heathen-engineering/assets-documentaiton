---
description: Have a question? Get an Answer!
---

# ⁉ F.A.Q

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="./">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/concepts/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Unity or Godot?

Either, Heathen's Steamworks was originally created as a Unity asset however we have ported the free [Foundation ](https://github.com/heathen-engineering/SteamworksFoundation)version to Godot and are in the process of porting the Complete version.

### What Version?

Godot (mono) 3.5 or later. \
To keep the code base between the two engines as close as possible and thus maintenance costs and bugs in check we use C# thus you need the "mono" version of the engine.

Unity 2020 LTS or later\
As per Unity's request we maintain all Unity assets on the oldest in support Unity version at current that is 2020 LTS

## Can this do X

If X is something the Steam API can do then yes.\
That is to say we cover 100% of the Steam API by virtue of being built on top of Steamworks.NET and extending that fundamental Steam API wrapper as opposed to trying to replaces it (as Facepunch does). As a result, if you can do it with Valve's Steam API then you can do it with Heathen's Steamworks.

### Code free?

Simple features such as initializing Steam API, loading and handling stats, achievements and leaderboards and even basic uses of the user's data such as fetching the users name, avatar image, etc. can in fact be done code free right out of the box.

If your [GitHub Subscriber](../../) our uGUI Tools take it a step further and can handle tasks like creating a friends list, clan chat and more code free right out of the box.

{% hint style="info" %}
Trying to do everything you can "Code Free" or with "Visual Scripting"?\
Read our article here on [Visual Scripting](../../company/concepts/development/visual-scripting.md) and maybe check out the rest of our Guides. Heathen is here to help you Do More and that means more than just selling you best in class Unity assets.
{% endhint %}

More complex features, and make no mistake Steam API is absolutely huge and has many many features some of which such as Steam Inventory can be incredibly complex ... these more complex features will always require you to "program" the logic that exploits them with respect to your game's needs. Depending on what tooling your using such as Bolt or other "visual scripting" tools you can still do it "Code Free" thanks to our tools and components layers.

### With the free version?

You can find a comparison of what is included in [Steamworks Foundation](./#feature-comparison) on the main page in this knowledge base.&#x20;

Keep in mind you can get instant access and a license to keep forever of Steamworks Complete ... and every other major Heathen asset for $10 by becoming a [GitHub Sponsor](../../) and yes you can cancel any time and keep what you downloaded and the license to use it.

### What about Microtransactions / Cash Shop?

Yes of course, Steam API handles MTX (micro transactions) via the Steam Inventory interface. Heathen's Steamworks Complete has robust tooling around [Steam Inventory](../../company/concepts/steam/steamworks/inventory/) which can greatly help any developer regardless of skill set.

> To reiterate as its often hard to believe, yes Steam API does MTX, yes it is [Steam Inventory](../../company/concepts/steam/steamworks/inventory/) that is used to do that.

## Can I try before I buy?

Yes its called [Steamworks Foundation](https://github.com/heathen-engineering/SteamworksFoundation) and is free to use. It has a limited feature set but is the same code used in the "full fat" Complete version.&#x20;

When ready you can get instant access and a license to keep forever of Steamworks Complete ... and every other major Heathen asset for $10 by becoming a [GitHub Sponsor](../../) and yes you can cancel any time and keep what you downloaded and the license to use it.

## Can I use this for commercial games?

Of course, have a look at some of the [great games that already use this](https://store.steampowered.com/curator/42461073-Made-with-Heathen).

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

1st yes, the networking tool you choose to use wont impact Steam API at all. Rather or not Steam API impacts it depends on rather or not that networking tool uses Steam Networking Interfaces. If it does then it needs to make proper use Steamworks.NET&#x20;

This is not something for us or Steamworks.NET to do its something for the networking tool in question to do. The following tools are known to have working proper integrations with Steamworks.NET or to not use Steam Networking at all.

### Fish Networking?

Yes: You can find more information in the [Networking Integrations](unity-engine/installation/networking-integrations.md) article.

### Mirage?

Yes: You can find more information in the [Networking Integrations](unity-engine/installation/networking-integrations.md) article.

### Mirror?

Yes: You can find more information in the [Networking Integrations](unity-engine/installation/networking-integrations.md) article.

### NetCode for GameObjects?

Yes: You can find more information in the [Networking Integrations](unity-engine/installation/networking-integrations.md) article.

### Photon (any variation)

Yes: Photon is its own platform, uses its own networking interfaces and has no impact on nor is it impacted by Steam API in any way that comes to mind.

### SpatialOS

Yes: SpatialOS is its own platform, uses its own networking interfaces and has no impact on nor is it impacted by Steam API in any way that comes to mind.
