---
description: For the Unity developer learning Unreal
---

# Unity to Unreal

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="success" %}
No you 100% do not have to learn C++ to create games in Unreal ... whoever told you that is full of 💩
{% endhint %}

So you are a Unity developer and you want to learn how to work with Unreal?

That's great, no matter your reasoning it is always useful to learn more about more tools and make no mistake an engine is just a game dev tool, it's not a religion, a marriage or a way of life. It's a tool, there are many, you should learn as much as you can and choose the right tool for the project and the team.

The articles in this section will explore the Unreal Game Engine, the typical design approaches seen with Unreal and will do it from the point of view of a Unity developer. The objective is to help you port as much of your knowledge and experience as possible into the early learning steps of Unreal giving you a boost on your journey.

### Approach

Unity and Unreal have two very different approaches to developing a game engine.&#x20;

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><h2>Unreal</h2></td><td><ul><li>More structured</li><li>More quality features out-of-the-box</li><li>Lot less you need to code from scratch</li><li>Logical split between Engine Code (C++) and Gameplay Scripting (Blueprints)</li><li>Scales up nicely e.g. likely easier for larger games, doesn't scale down much, mobile is doable but won't be lightweight</li></ul></td></tr><tr><td><h2>Unity</h2></td><td><ul><li>Sandbox-esk in structure</li><li>Plenty of not-built-in things you will need to solve for</li><li>Generally need to author more code to get things going</li><li>Everything is done in C#, systems, tools, gameplay logic all of it</li><li>Scales down very nicely (mobile, web, etc.) but might struggle to scale up</li></ul></td></tr></tbody></table>

## Design

Unreal has a "way" to it, because Unreal has so many tools, features and systems available to you right out-of-the-box you probably want to make yourself aware of what that "way" is and adjust your design to make use of it, not fight against it.

{% embed url="https://www.youtube.com/watch?v=iQ3c-lrHO7o" %}

Beyond those handy tools, in Unreal fundamental concepts of a game are already defined and built in as part of the engine.

* Game Instance
* Game Mode
* Actor
* Pawn
* Character
* Controller
* etc.

Understanding the relationship between these objects and how best to leverage the inherent design of Unreal to the advantage of your game is key to success. Where in Unity if you wanted to do something you likely just start trying to do things, in Unreal I would STRONGLY recommend you research and see if Unreal has a feature/tool/system that does this already (it often does). This doesn't mean you should always just use the native system but you should never ignore that there is one.

### Game Objects

When you first open Unreal it might be tempting to think of Actor as GameObject ... dont

In Unity, we have a frankly bad habit of nesting GameObjects and even using them as folders for organizational purposes.

A level in Unity is really a tree structure of GameObjects where some objects have components attached causing logic to run. The organization of GameObjects impacts transform logic as well as execution order and even whether or not the object is even active.

In Unreal, we don't nest things, an Actor is not like a GameObject with children below it that we would turn on and off.&#x20;

A level in Unreal is more like a flat list of Actors, each actor represents just that ... an actor in the world with a visual, behaviour, some data, etc.

Actors may be composed of components and may have relationships with other actors but they are not generally "parented" or grouped. In general, each Actor is functionally independent, we add or remove actors and components to achieve the needs of the game. We use systems and tools to facilitate level design.

If you have used Unity's DOTS you find that an Actor is much more like an Entity than it is a GameObject

## Development

Let's address the🐘elephant🐘 in the room, C++ vs C# and Unreal's Blueprint system.

The video linked below will help you understand how Unreal treats C++ vs Blueprints and coming from Unity this is a very different approach than you are used to but it's not a hard one and it's one you will very likely come to love.

To put your main fears to rest let me go ahead and say:\
**No:** you do not -have to- code your game in C++\
**No:** you do not -have to- code your game in Blueprints

You will not need to write anywhere near as much logic of any kind for most Unreal projects compared to the amount of custom/bespoke logic you need to create for a similar Unity project. This is down to the age and maturity of the engines. Unreal just simply has more structure and tools in its toolbox that are more flexible and very often will do what you need how you need it with a bit of simple configuration. In contrast with Unity when we need to do something, 9 times of 10 we make a quick script in C# to do that, or use a script someone else had already made.

{% embed url="https://www.youtube.com/watch?v=VMZftEVDuCE" %}

## Networking

Nowhere is the difference in game development more apparent between Unreal and Unity than in networking.

Unreal itself is fundamentally designed to be a multiplayer game engine. Out-of-the-box with no additional anything added to it, you can start a multiplayer session, right with the sample scenes. If you want to make a variable replicate over the network it really is as simple as toggling a tick box on that variable.

In contrast, Unity is not, with Unity your first step is to decide how you want to handle networking. The most common approach is an HLAPI such as NetCode for GameObjects, Mirror or FishNetworking but there are other options as well. Then for everything you might want to replicate over the network, you must code in C# or use existing scripts everything from scratch.
