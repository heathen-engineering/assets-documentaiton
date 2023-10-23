---
description: For the Unity developer learning Unreal
---

# 🔀 Unity to Unreal

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

So you are a Unity developer and you want to learn how to work with Unreal?

That's great, no matter your reasoning it is always useful to learn more about more tools and make no mistake an engine is just a game dev tool, it's not a religion, a marriage or a way of life. It's a tool, there are many, you should learn as much as you can and choose the right tool for the project and the team.

The articles in this section will explore the Unreal Game Engine, the typical design approaches seen with Unreal and will do it all from the point of view of a Unity developer. The objective is to help you port as much of your knowledge and experience as possible into the early learning steps of Unreal giving you a boost on your journey.

## Approach

Unity and Unreal have 2 very different approaches to developing a game engine.&#x20;

{% hint style="info" %}
I like to think of Unity as Linux and Unreal as Windows ... guess that makes Godot Mac?\
\
by that I mean Unity is flexible and will let you do whatever however and probably will still run. Unreal in contrast has a "way", you can go against that way but it takes effort to do so and might really break things.\
\
Unity like Linux though requires you to do a TON more yourself, from scratch to deliver a given result.\
\
Unreal like Windows is ready to go right now with out-of-the-box tools and systems and can achieve so much with comparatively little bespoke work.
{% endhint %}

I personally find Unity far faster and easier to write code for which is a good thing because in Unity you just need to write a whole lot more from scratch to bring your project to life. Unity is faster because it's far less rigid, you can more or less throw whatever you want at it however you want and it will do a thing. It may not be efficient, it may not be what you want but it will do the thing.

Unreal is more rigid and has a "Way" things should be done for most things. It's not that you can't change that approach but it is a hell of a lot more work to do it the "non-Unreal" way than it is to swallow your pride and do it the Unreal way. This I think makes Unreal far more friendly to designers and makes engineers/programmers have to work a bit harder. It also means you need to learn the right way to do a thing and not simply fling copy and paste code at it expecting it to work... so 99% of how most Unity devs get started.

While Unreal is more rigid it's also far more complete, anything you can think of has very likely already been done in Unreal and probably has a ready-built system, node or approach defined in the engine. This means for just about anything you might want to do you can at least prototype it out with just a few clicks.

Take the double jump for example, to do this in Unity we would .. well there are countless ways you could do it but you will be doing it from scratch, testing keyboard input, applying force, etc.

In Unreal Double Jump is a blueprint node, you drag and drop and it's done. That node isn't from the asset store or some random dev, that node is part of the engine along with the 1st person, 3rd person, top-down, etc. character controllers and a ton more. You can configure that out-of-the-box implementation to tune it or if double jump is just really important to your game and you need to hand code your very own version, you can copy the code of the built-in and go from there ... yes Unreal provides its full source.

### C++ & Blueprints

Right out the gate let's address the elephant in the room, C++ vs C# and Unreal's Blueprint system.

The video linked below will help you understand how Unreal treats C++ vs Blueprints and coming from Unity this is a very different approach than you are used to but it's not a hard one and it's one you will very likely come to love.

To put your main fears to rest let me go ahead and say:\
No you do not -have to- code your game in C++\
No you do not -have to- code your game in Blueprints

You will not need to write anywhere near as much code of any kind for most Unreal projects compared to the amount of custom/bespoke logic you need to create for a similar Unity project. This is down to the age and maturity of the engines. Unreal just simply has more structure and tools in its toolbox that are more flexible and very often will do what you need how you need it with a bit of simple configuration. In contrast with Unity when we need to do something, 9 times of 10 we make a quick script in C# to do that, or use a script someone else had already made.

{% embed url="https://www.youtube.com/watch?v=VMZftEVDuCE" %}

### Networking Example

Nowhere is the difference in game development more apparent between Unreal and Unity than in networking.

Unreal itself is fundamentally designed to be a multiplayer game engine. Out of the box with no additional anything added to it, you can start a multiplayer session, right with the sample scenes. If you want to make a variable replicate over the network it really is as simple as toggling a tick box on that variable.

In contrast, Unity is not, with Unity your first step is to decide how you want to handle networking. The most common approach is an HLAPI such as NetCode for GameObjects, Mirror or FishNetworking but there are other options as well. Then for everything you might want to replicate over the network, you must code in C# or use existing scripts everything from scratch.

### Flexibility

Both approaches have the same level of flexibility in terms of letting you change how things are done. For example, if you want to use Steam Networking Sockets in Unreal then you need to use a NetDriver suited for that (Heathen provides one of course 😉).

In Unity, you would use a transport for your networking solution of choice that worked with Steam Networking Sockets ... and again Heathen has you covered 😉

The difference is that with Unreal the "HLAPI" aspect is 1st party, that is Epic Games has built that into the engine. They have also created a number of "Online Subsystems" to get you up and running right away with various platforms and of course, developers like Heathen have created tailor-made solutions such as Heathen's Steamworks Complete which is available for Unity or Unreal.
