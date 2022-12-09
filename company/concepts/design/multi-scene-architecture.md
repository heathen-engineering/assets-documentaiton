---
description: >-
  Understanding the concepts behind multi-scene architecture in the Unity game
  engine
---

# 🤹 Multi-Scene Architecture

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Often, and the name of the thing reinforces this notion; we as developers think of a "scene" as a physical area in our game, similar to a stage where our actors can play. This notion however is rather limiting and not at all true with regards to what a scene is in terms of the Unity Engine.‌

A scene is more accurately thought of as a folder or collection of GameObjects. How you choose to break your "scenes" up should not typically be based on physical local as much so as load order or put different when are these things of use to have in memory.‌

To determine what should be loaded when we need to understand the concept of "Scope", that is we should load all the objects that are "in scope" or are expected to be "in scope" soon and unload any objects that are "out of scope".

## Why Though?

### Efficiency

* More and smaller scenes are faster to load, easier to unload and offer more granularity in control of what you have loaded and when. \
  Compared to having a few large scenes which take longer to load, and have to be loaded in the entirety before use.\

* Common objects that would appear in all scenes can be defined once in one scene that simply persists. \
  Compared to having each individual scene defining these same objects further increasing the work that Unity must do to load initialize and eventually unload a given scene.

### Maintainability

* Scenes can be broken up by geographic area in your game or event by function, e.g. an environmental set of scenes, a UI/HUD scene, etc. meaning you can load into the editor and work on only the subset of objects relevant to you and your task at the moment.\
  Compared to having a monolithic scene that has everything in it. Slower to load, slower to save, harder to find specific objects needing more use of organizational objects (empty GameObjects acting like folders)\

* Reduce duplication. why should every scene have a camera, HUD, input system, event system, etc? Define these once in a scene that persists as needed.\
  Compared to every scene having its own copy, meaning a change to say camera FOV must now be applied to every scene, exponentially increasing your workload and increasing the likelihood you forget one, introducing bugs that aren't easy to detect as they don't throw errors.

### Design Time Organization

* Breaking up objects across scenes by completed objects away from WIP (work in progress) scenes can help reduce the cost of on going development by reducing the likelihood of introducing bugs into previously completed work. The idea here is your WIP objects that are actively being worked on live in their own scene, so changes to them do not unintentionally impact completed objects in other scenes.\
  In a monolithic scene structure, it's all too common to unintentionally change a structure or disable something for testing of some WIP object, forgetting you did so and that bug slipping through unnoticed for a prolonged period of time, thus causing run on issues in later development.\

* When working in a team, collaboration is always a point of challenge. Splitting scenes apart based on work delegation can reduce conflicts and greatly simplify change management. This can be coupled with WIP (work in progress) scenes enabling parallel development while minimizing the complexities typical in such cases.\
  Compared to a monolithic scene where very often work must be stopped by some team members while others finish some change. A Unity scene is a single file after all, and simultaneous collaboration on a single scene is a challenge even for a vetted engineering team.

## Determining Scope

### Physical Location

One obvious way to determine the relevant scope of an object to load is its physical location. This though is only really relevant for things that do not move.  Things where the player moves closer to or further away from the object thus bringing the object into or out of scope.

{% hint style="info" %}
You will often see the term "Page" or "Pages" to refer to collections of objects defined by location, the idea being the player is on a page and we load that page and the 8 other adjacent pages.

A more natural term might be "tile" like the tiles on a floor. You are at any given time standing on 1 tile. You are likely to move to one of the adjacent tiles (8 possible options) so this system gives us an easy way to determine what "pages" e.g. what scenes we should consider "in scope" and thus load.
{% endhint %}

This approach of local based scope does not apply to MOBs (literally stands for Mobile Object) as these objects can move them selves in or out of scope. They can for example chase the player across many "pages" or scenes and so loading them in or unloading them based on some location would cause them to pop out of existence as they chased the player. The player its self is another example of such a mobile object.

### By Use

Most objects wont be loaded based on location, but rather based on use. For example regardless of physical location there are some objects we just always need in memory, and these we want to load at the start of the game and never unload, e.g., [bootstrap](bootstrap-scene.md) objects such as:

* The camera
* The Audio Listener
* The Event System
* The Input System
* Game systems such as&#x20;
  * Network Managers
  * Steamworks Behaviors
  * etc.

The above are objects that are always present, but there are also objects that are persistent through various phases of the game, again regardless of the physical location of the player for example the HUD or GUI the player uses during gameplay would be persistent regardless of location but wouldn't be in scope while the player is in the main menu.

### Dynamically

One of many buzz words, meaning the system picks something on its own each time. This is most often seen with loading screens, title/main menu scenes or similar passive situations, it however can also be used in "dynamic world design" hence the choice of header for this section.

{% hint style="info" %}
While this approach can be the bases of an entire game it’s also an effective way to spruce up your title scene, loading screens and any area that would otherwise start to feel stale to your player if left static.
{% endhint %}

The basic concept is you define your "pages" or "tiles" that is your bite sized chunks of GameObjects that Unity calls scenes to be loaded such that your system can select from a set of viable options, these options informed by player actions or other conditions in the game or simply  on a loop such that every visit to the title screen shows a different bit of eye candy.

{% hint style="info" %}
This differs from "procedural" or "random" world creation in that the system does not pre-determine the world state on initial load. Instead as the player progresses through the system adjusts the viable options that can be loaded next, thus the next "pages" loaded are determined not by simple random generation but by the actions the player has taken.

Did the player loot all the treasure? Perhaps you want to keep the challenge up and their gold supply down so exclude pages that have a higher gold generation chance.

Did the player find a secret? Perhaps that adds special pages to the possible options increasing the chance the player will discover something rare.
{% endhint %}
