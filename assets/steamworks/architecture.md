---
description: Ogres have layers ... and so do we
---

# 🧅 Architecture

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="./">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/concepts/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Heathen's Steamworks is built in layers of abstraction providing you with a rang of options for doing most anything. Rather your looking for a code free production ready drag and drop solution ... or a battle tested and hardened tool kit to empower and accelerate your engineering/programming team ... we help you Do More!&#x20;

{% hint style="danger" %}
:fearful: I'M OVERWHELMED AND CONFUSED !?!?!?!?!?

Take a deep breath and relax, the layered approach isn't making things harder it simply gives you more control and more options.&#x20;



You can use any level of tool you like, mixing and matching as you see fit, to include using the raw Steam API and all of our tools will simply work with you. Everything we provide is built upon the lower levels right down to the raw Steam API so there is no black magic to get in your way.



We provide these layers of tools so that you can always do what you need with minimal effort be that production ready tools for your designers, or API wrappers that empower and accelerate your engineers.&#x20;



Rather your looking for code free drag and drop solution to fill some common need

Or looking for a simpler easier to use set of tools to help you create your custom features

Or just looking for a tool to take care of the boiler plate code and then get out of your way

\
Heathen's Steamworks has tooling for you
{% endhint %}

## Layers

From the highest level (most abstract and typically simplest to use) to the lowest level (most "native" and typically most flexible to use).

{% hint style="info" %}
### Prefabs

_**Unity Only**_\
Our prefabs use 1 or more of our components to give you a production ready working tool to meet a specific need. From Leaderboard Lists, To Party Lobby we have drag and drop code free, ready role tools to meet many common needs and are adding new one all the time.
{% endhint %}

{% hint style="info" %}
### Components

_**Unity Only**_\
Component scripts that can be added to GameObjects exposing common features and functionality to the Unity Inspector. These components expose the events, callbacks and functions such that you can easily connect them to your own GameObjects, scripts and systems.
{% endhint %}

{% hint style="info" %}
### Objects

_**Unity Only**_\
ScriptableObjects that encapsulate Steam artifacts and concepts allowing you to easily reference them in your own scripts and with our components. This lets you create a reference to say a stat, achievement or leaderboard and drag and drop that leaderboard, stat or achievement from your Steam Settings onto your GameObject&#x20;
{% endhint %}

{% hint style="info" %}
### Data

Light weight structs that encapsulate Steam concepts simplifying use of common Steam features like Lobby, Clan, Stat, Achievement, Item, Leaderboard and much more. These structs are implicitly convertible to and from the Steam native IDs and the underlying primitives.&#x20;

\
This means you can convert a simple string to an achievement and use its features

```csharp
AchievementData myAchievement;
myAchievement = "my_achievement_API_name";
myAchievement.IsAchieved = true;
```
{% endhint %}

{% hint style="info" %}
### API

Wraps the underlying Steam tools making it more "Engine Centric" for Unity as an example this means we wrap all of the C style callbacks and callresults with UnityEvents&#x20;



Our API makes Valve's Steamworks far less cryptic and far more C# and engine relevant enabling your engineers and programmers to work with it much more natively than with the raw Steam API.\
\
We have also simplified many multi-step processes and concepts, provided request queues and other quality of life features ontop of the raw Steamworks interfaces. Even if your a Steamworks pro, our APIs are all battle tested, robust, efficient and well documented and maintained.
{% endhint %}

{% hint style="info" %}
### Steamworks.NET

A 1-to-1 C# conversion of the native Steam API.&#x20;

Steam API is written in C/C++ using style that is not typical for modern game development.

Steamworks.NET does not change or adapt anything here, it simply acts as a true to form C# .NET wrap of the native Steam API. Consequently this means Valve's documentation is fully applicable to it and anything built for the native Steam API will just work with Steamwork.NET pending only a language conversion.
{% endhint %}
