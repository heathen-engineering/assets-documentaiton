# Welcome

## Where to Get It <a href="#where-to-get-it" id="where-to-get-it"></a>

All our tools are available via [**GitHub Sponsors**](https://github.com/sponsors/heathen-engineering) or [**Patreon**](https://www.patreon.com/HeathenEngineering).&#x20;

## All Tools, Yours Forever!

{% hint style="success" %}
### Get a permanent, lifetime license to all of our tools for all supported engines ( Unity & Unreal ). Pay once, and they’re yours to keep. No DRM, no lockouts, no strings attached.
{% endhint %}

**Prefer Traditional Stores?**

Get one year of updates and professional support for just the tools you want via the [Unity Asset Store](https://assetstore.unity.com/publishers/5836) or [FAB](https://www.fab.com/sellers/Heathen%20Engineering).

{% hint style="info" %}
_Purchases through the Unity Asset Store or FAB follow their standard licensing terms, which, at the time of writing, are per-user. The version you buy is yours permanently. Each year, a new major release will be available as an update and support package, offered to existing users at 20% of the base price. You may continue using any previous version indefinitely. Older versions are not revoked or disabled._
{% endhint %}

***

## Do More with Heathen

### More than just another API wrapper!

Heathen's Toolkit is a robust kit of editor tools and extensions, proven game systems and extensive guides and articles that cover not just every function & feature of the plugin but go beyond into guides & articles on every facet of being a Steam Developer and Game Developer in general. This is all supported by our team of passionate engineers & our community of thousands of game developers who have shipped hundreds of games on Steam.

## Key Features

### Knowledge Base

Even if you never use our tools, this Knowledge Base is the best resource for any game developer planning to ship on Steam.

We cover every aspect, not just of the Steamworks SDK but the Steam platform itself, including but not limited to setting up your store page, working with the community hub, understanding the discovery queue and of course a full breakdown of every feature of the Steamworks SDK.

### Full Coverage

No half measures, no black magic, every feature of the Steam API is available as defined by Valve with no shortcuts or skipped features, and they are all fully supported by our easy-to-use and robust tools with full source code included.

Whether you are a veteran Steam developer looking to save time and reduce maintenance costs or a hobbyist hoping to demystify the powerful but often cryptic Steamworks SDK, Heathen has you fully covered on Unreal and Unity, with Godot support a work in progress.

### Engine Native

More than just another API wrapper means just that, we go above and beyond simply exposing the Steamworks SDK endpoints to you in code and scripting interfaces (C#, Blueprints, etc.). Heathen's Toolkit for Steamworks SDK is a toolkit of proven, trusted, efficient and well documented and supported systems, frameworks, widgets, prefabs, tools, guides, approaches and more.

We of course do expose every endpoint, enumerator and interface in code (C#, Blueprints, etc.). So we are also a wrapper that makes the Steamworks SDK feel native to the engine you choose and in the way you choose to work with that engine.

Then we build on top of that low-level one-to-one engine-specific wrap, making it trivial to connect Steam-centric concepts to your Engine's native concepts e.g. textures, event systems, data type limitations, etc.

Then we build on top of that with systems, widgets, prefabs and templates that work with your engine's concepts to address common use cases and boilerplate needs in a manner appropriate for the engine you are working on. Initialization, Save Game, Data Management, etc. and we enable networking solutions common to your engine of choice to do the same e.g. NetCode, FishNet, Mirror, NetDrivers, etc.

## Battle Tested

{% embed url="https://store.steampowered.com/curator/42461073-Made-with-Heathen" %}

Trusted by [thousands of developers](https://discord.gg/6X3xrRc), we have been hard at work on this tool for more than a decade. [The Steam Curator link above](https://store.steampowered.com/curator/42461073-Made-with-Heathen) is just a few of the works our community have published, covering many genres and demonstrating a wide range of examples from small passion projects to major commercial products.

Toolkit for Steamworks SDK is a reliable, proven solution to help you Do More with your game's on Steam.

## Built for You

Our tools are built in layers from powerful APIs and Frameworks up to code-free solutions. No matter your need, skill level or discipline, our tools can help you Do More!

{% hint style="success" %}
Whether you're new to Steam or game development in general or maybe a seasoned veteran well capable with the Steam APIs, Heathen’s Steamworks can greatly accelerate your project and help you produce a more robust product that better leverages the services offered by Valve.&#x20;
{% endhint %}

## Heathen vs Steamworks.NET

Unity Healthen's Toolkit for Steamworks SDK is built on top of [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET). The [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) project is designed to be a direct 1 to 1 wrapper around Valve's Steam API, wrapping the native C and C++ interfaces up in a C# plugin.

{% hint style="success" %}
[Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) is authored by [**Riley Labrecque**](https://github.com/sponsors/rlabrecque) be sure to check out and support his great work! You can pop over to his [sponsor page](https://github.com/sponsors/rlabrecque) if you are interested.
{% endhint %}

[Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) gives the best access to Valve's APIs and does so true to the original, so that the original documentation and decades of community guidance are still applicable.&#x20;

The drawback to [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) is that it is true to the original API using programming styles and approaches foreign to most game developers and very clunky at best to use in Unity or Godot scripting.

Heathen has extended every relevant interface in Steamworks.NET, delivering a simpler, more robust tool set. Every drop of power of the native Steam API / Steamworks API is still available to you should you have the need.

Heathen's Steamworks does not replace [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) - it builds on top of it and provides you with a set of battle-tested and developer-approved tools and systems written with Unity in mind.&#x20;

## Heathen vs Facepunch

Facepunch is another C# wrapper just like Steamworks.NET however, unlike Steamworks.NET it does not attempt to remain true to the original API as a result, the existing community and documentation around Steamworks are less applicable. &#x20;

Facepunch's stated goal is to make a C#-focused wrapper that exploits/leverages the benefits of C#. This makes most of the code you would need to write shorter / more C# programmer-friendly. It, however, also makes it alien to Valve's documents and its wider community and while Unity uses C# as its main scripting language, it does so in a "Unity" way for example, C# would use event delegates; in Unity, we use UnityEvents.

Heathen does similar in that we are here to make the Steam API more friendly to a specific audience, only we are Unity-centric, not just C# centric. We have wrapped the complexities of Steamworks.NET, making it quick and easy to integrate for C# programmers, Unity-specific programmers, Unity designers and hobbyists who prefer to use tools like Bolt or work through inspectors to get the job done. We chose to build on top of Steamworks.NET so that the dev who wants/needs to can still leverage the decades of community guidance on the source API, only needing to convert C/C++ to C#.

Because we are built on top of Steamworks.NET, which is itself a true-to-form wrapper around the native Steam APIs many tools, assets, etc. built for Steamworks.NET or Valve's original Steam API simply work, that is not the case for Facepunch which often requires its own flavour of a tool to work.

## Heathen vs Online Subsystem Steam

Put bluntly [Online Subsystem Steam](https://docs.unrealengine.com/5.3/en-US/online-subsystem-steam-interface-in-unreal-engine/) is an incomplete solution. It does not cover the full Steam API and is limited to a handful of modules, what it does cover it only partially covers.

Heathen's Toolkit is a complete integration of every aspect of Valve's Steamworks with the engine. It goes well beyond a simple API wrapper and provides you with ready-made and proven tools. The full Steam API is exposed to you in both C++ and Blueprint Functions, we also provide you with a set of common-use UI Widgets and Unreal-centric tools like our Steam Remote Storage Save Game base class, Steam Game Instance and more.

## Heathen vs Steam Core

Steam Core is a plugin available from the Unreal Marketplace and is "another Steam API wrapper". It provides more coverage than you get with Epic's own Online Subsystem Steam, but doesn't cover the full Steam API. It also (appears) to make improper use of Steam API in a few key areas for example its approach to Steam Remote Storage (aka Steam Cloud) is to save the game to the disk using Unreal's Save Game and then read that file from the disk to save it to Steam Remote Storage ... this is exactly what Valve says you shouldn't do as you will end up with sync issues, it also doubles the disk space the save uses since Steam Remote Storage also writes the file to disk before syncing to Valve's backend.

The major difference between Heathen and frankly any other option is that Heathen has been doing this for over a decade, we have supported thousands of developers shipping hundreds of games on Steam. Our tools are well-designed and adhere to Valve's and the engine's best practices, our tools are more than just a Steam API wrapper, they let you leverage our extensive experience with the Steam API and Steam platform.
