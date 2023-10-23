---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
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

# Unreal

{% hint style="success" %}
Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The articles within are specific to Unreal and include the engine-specific tools and systems unique to the Unity version of the package.&#x20;

## Comparison

<table data-full-width="true"><thead><tr><th width="381.5">Features</th><th width="303">Online Subsystem Steam</th><th width="319">Complete</th></tr></thead><tbody><tr><td>License</td><td><a href="https://docs.unrealengine.com/5.3/en-US/online-subsystem-steam-interface-in-unreal-engine/">Free</a><br><em><mark style="color:yellow;">Warning Online Subsystem Steam is out of date with modern Steam API.</mark></em><br><em><mark style="color:yellow;">It's related Steam Sockets NetDriver is even more so out of date.</mark></em></td><td><a href="../../become-a-sponsor/">Sponsor ($15)</a><br>Unreal Marketplace (coming soon)</td></tr><tr><td>C++ API Supported</td><td>- Old Steam API version</td><td>✔ always up to date, and upgradable without requiring a full engine recompile</td></tr><tr><td>Documentation</td><td><a href="https://docs.unrealengine.com/5.3/en-US/online-subsystem-steam-interface-in-unreal-engine/">Minimal</a></td><td>This Knowledge Base</td></tr><tr><td>Support</td><td>Community</td><td>Dedicated + Community</td></tr><tr><td>Steam Networking Sockets</td><td>- Old Steam API version, dependent on Online Subsystem</td><td>✔ full-featured NetDriver, latest Steam API version, no dependency on an Online Subsystem</td></tr><tr><td><h3>Editor Tools</h3></td><td></td><td></td></tr><tr><td>Achievement UI Tools</td><td></td><td>✔</td></tr><tr><td>Build Upload Tool</td><td></td><td>Packaging Tool Coming Soon</td></tr><tr><td>Chat UI Tools</td><td></td><td>✔</td></tr><tr><td>Group / Clan UI Tools</td><td></td><td>✔</td></tr><tr><td>User Profile Tools</td><td></td><td>✔</td></tr><tr><td>Leaderboard UI Tools</td><td></td><td>✔</td></tr><tr><td>Lobby UI Tools</td><td></td><td>✔</td></tr><tr><td>Debugging Tools</td><td></td><td>✔</td></tr><tr><td><h3>API Extensions</h3></td><td></td><td></td></tr><tr><td>Application</td><td>- Partial</td><td>✔ + Blueprint Integration</td></tr><tr><td>Authentication</td><td>- Partial</td><td>✔ + Blueprint Integration</td></tr><tr><td>Big Picture</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Groups / Clans</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>User / Friends</td><td>- Partial</td><td>✔ + Blueprint Integration</td></tr><tr><td>Steam Input</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Inventory</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Leaderboard</td><td>- Partial</td><td>✔ + Blueprint Integration</td></tr><tr><td>Matchmaking</td><td>- Partial</td><td>✔ + Blueprint Integration</td></tr><tr><td>Overlay</td><td>✔</td><td>✔ + Blueprint Integration</td></tr><tr><td>Parties</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Remote Play</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Remote Storage (cloud)</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Screenshots</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Stats &#x26; Achievements</td><td>- Partial</td><td>✔ + Blueprint Integration</td></tr><tr><td>UGC (Workshop)</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Utilities</td><td></td><td>✔ + Blueprint Integration</td></tr><tr><td>Voice</td><td>✔</td><td>✔ + Blueprint Integration</td></tr></tbody></table>

### But Online Subsystem Steam?

{% hint style="success" %}
Heathen's Steamworks Complete will save you hundreds if not thousands of hours and enable you to exploit every feature Valve's Steamworks provides easily, efficiently and in a stable and robust manner.
{% endhint %}

[Online Subsystem Steam](https://docs.unrealengine.com/5.3/en-US/online-subsystem-steam-interface-in-unreal-engine/) is a barebones integration of the basics and is built on an outdated version of Steam API. Know that any "Online Subsystem" from Unreal is an attempt at shoehorning a given platform's features into the form expected by Unreal. This means you cannot take full advantage of the platform, you cannot leverage all the features available and you must use the limited integration in the Unreal-defined manner, in the case of Steam API this is hugely limiting.

Setting aside the poor documentation for Online Subsystem Steam and the fact that it's on an older version of Steam API, it also simply lacks many of Valve's most valuable Steamworks features and what is covered is only partially covered. The fact that it is outdated also presents risks regarding authentication and similar security features.

Heathen's Steamworks Complete is as its name suggests a complete solution. Our plugin is kept up to date with Valve's Steamworks SDK and the version of the SDK used can be changed by you without requiring a full recompile of the whole engine.

More than "Just Another Steam API Wrapper", Heathen's Steamworks Complete exposes the whole of Steamworks in C++ code as well as Blueprint functions and bindable events. We deliver ready-to-use widgets and blueprints for common use cases and editor tools like the Steam Build Tool. We have created production-ready Unreal Engine-centric objects to make working with Steam API a more engine-native experience (Steam Game Instance, Steam Remote Storage Save Game, etc.)

Beyond the engine plugin, we also provide an extensive knowledge base that goes beyond simply listing interfaces and provides actual guidance for not just technical features but every aspect of the Steam platform. We also foster a rich community of thousands of game developers that have shipped hundreds of games on Steam and of course, we provide support for our asset and your use of it.

### Steamworks Complete Plugin

{% hint style="info" %}
We are in the process of migrating Steamworks Complete to Unreal at times the documentation may be ahead of the plugin or behind a bit ... for any questions see our [Discord](https://discord.com/channels/463483739612381204/1153799474620137483).
{% endhint %}

* Full native Steamworks SDK for both C++ and Blueprints\
  Unlike Unreal's existing solutions `Steam Core` and `Online Subsystem Steam`, Heathen's Steamworks Complete is the full Steamworks SDK, every feature, every endpoint, and every callback. If Steam can do it ... you can do with with Heathen's Steamworks Complete.
* Steamworks Networking Sockets NetDriver\
  Unreal's built-in Steam Sockets plugin is just as out of date as its Online Subsystem Steam and sadly is dependent on Online Subsystem Steam. We have created an up-to-date NetDriver with -no- dependency on an Online Subsystem.
* Battle-tested systems\
  10+ years developing for Steam supporting thousands of developers shipping hundreds of games. Heathen's Steamworks Complete is much more than just another Steam wrapper. We handle the boilerplate for you, we provide game-ready systems for common use cases, and we enable you to Do More!
* Rich Knowledge Base\
  Steam API is known for its ... sparse ... documentation. Heathen steps in and delivers more than lists of functions and members. We have guides, tips, tricks, best practices and more not just for our own tools but Steam as a platform and game development in general. We are your go-to resource.
* Live Community / Support\
  Join a community of fellow developers working across multiple engines. We provide live support and real-time conversation supporting not just our own tools but fostering a helpful and supportive community around Steam and game development in general.

### Work Your Way

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h2>C++</h2></td><td>Simple full access to the native Steam APIs in C++ with no faffing about required.</td><td></td></tr><tr><td><h2>Blueprints</h2></td><td>Access every function and event available through Steam API in Blueprints no C++ required.</td><td></td></tr><tr><td><h2>Tools</h2></td><td>Build Tool, prebuilt widgets for common use cases and much more.</td><td>Do More with Heathen!</td></tr></tbody></table>
