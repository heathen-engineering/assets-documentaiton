---
description: >-
  Before you code or even design the solution ... you define the problem and how
  to prove its solved.
---

# ✏ Writing Formal Tests

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article will help you break down the process of creating tests for your game or app in a structured and formal way. Note that testing is not limited to the code and is a rather broad topic covering many levels of the design and development process. In this article we break down the creation of your formal test cases. These are the tests that you must "pass" to know the game is complete and of a sufficient level of quality to be released.

### When

Their are different schools of though as to when tests should be written. Most professional software engineers will tell you that you should define your test before your software design and thus much before you start writing any code. The act of creating the tests that will prove a thing is or is not complete to the quality standard is the best way to understand what you need to build before you try to actually build it.

That said most game development is less "engineered" and more "hacked" and hopefully later cleaned up in production. As a result tests are usually defined at the end of the [preproduction](../fundamentals/development-phases.md#preproduction) phase and very likely will be expanded, reduced or otherwise modified over the [production ](../fundamentals/development-phases.md#production)phase of the game. Ideally the bulk of your "engineering" will be done with good test cases driving that technical design and implementation.

## Define

Before you can write a test to prove something you need to have a structured understanding of what it is ... or rather what it should be. Their are a ton of ways to go about this but most are some variation of the following

### Stories

As you close in on the end of preproduction you should have a really good idea of what the resulting game should be. As with anything their are multiple ways to accomplish this, a common approach is via "User Stories" or "Player Workflows", both effectively meaning to "map" the players path through your game.&#x20;

As you define these paths you can more effectively identify the major areas and features of your game to build your tests around. With an understanding of those "key features" you can pick out key "user story" points that define those features it is those "story" elements you will use as the bases for writing your tests. The following bullet list shows a hypothetical breakdown of a game, this splits out the game into areas composed of features and below each feature highlights the "story" points that define the feature.

The example is of course not complete and is just a demonstration of the hierarchal organization created by this process.

* (area) System Level
  * (feature) Steam Initialization
    * (story) User Settings requires Steam API to read stored settings data off Steam Remote Storage.
    * (story) Validation Process requires Steam API in order to validate Steam initialized as the expected App ID
  * Exception handling/reporting (feature)
    * (story) ...
  * Feedback gathering (feature)
    * (story) ...
  * Splash and Loading (feature)
    * (story) ...
* Main Menu (area)
  * (feature) Quick Match
    * (story) Player in a group with a friend can with a single gesture find a suitable lobby for them and their friend or if none found create a suitable lobby
    * (story) Player not in any group can with a single gesture find a suitable lobby or if none create a suitable lobby
* Single Player (area)
* Multi Player (area)

### Environments

You will define a selection of environments you expect your game or app to execute on. For a typical game project an environment definition will describe.

* Hardware configuration such as RAM, CPU and Graphics
* Operating System
* Any relevant drivers or supporting software
* Any relevant periphery such as monitor resolutions and ratios, controllers, etc.

Ideally you would have an understanding of all significant environments e.g. every possible variation however this is not usually practical or in many cases even possible. You should focus on having environments that describe your "upper and lower bound" meaning the least powerful and most powerful machines you expect your game will run on. In addition to the upper and lower you should try and represent a "most common" slice of what you expect your game will be ran on.&#x20;
