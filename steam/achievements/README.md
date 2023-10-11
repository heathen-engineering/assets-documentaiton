---
description: Be better than "killed 10 rats"
---

# 🏆 Achievements

{% hint style="success" %}
#### Like what you're seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Achievements are a simple and traditional feature for games that can help drive player engagement. While they are simple to implement (make work) coming up with a good achievement design is not so simple. You could of course :face\_vomiting: forth random achievements like "Played 15 min", "Logged into the game", and "Pressed the spacebar"; but these are often time harmful to the game and not helpful.

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/features/achievements](https://partner.steamgames.com/doc/features/achievements)

</details>

## Quick Start

First you need to create your achievements on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

### Create

Log into your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="Techincal Tools"><figcaption></figcaption></figure>

From there select the Stats & Achievements > Achievements option and create your new achievements.&#x20;

Make note of the value you use in the API Name field. You will use it when working with achievements in code.&#x20;

In Unity, if you prefer to work with Achievements via an object reference then you can use our [AchievementObject ](../../heathens-steamworks-complete/unity/scriptable-objects/achievement-object.md)which is a Unity ScriptableObject that can be referenced and accessed like any other Unity Object.

<figure><img src="../../.gitbook/assets/image (1) (6).png" alt="Achievement test"><figcaption></figcaption></figure>

### Publish

You \*\***MUST**\*\* publish your changes in Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

### Use

Use your achievements ... how? depends on the tools and engine you choose set the [Unity Achievements](unity-achievements.md) and [Unreal Achievements](unreal-achievements.md) articles for more information.

## Using Achievements

The first thing to understand is that with stats and achievements, the process of setting them in two steps.

1. You assign the value&#x20;
2. You store the changes in the backend

{% hint style="success" %}
Understand that not every game needs achievements, that if you're going to have achievements they should be part of the game and not an afterthought you bolted on because why not? Meaningless achievements can harm the user experience by breaking immersion or simply drawing attention away during gameplay.

Following are some ideas for meaningful achievements and how you might tie those achievements into other aspects of your game.
{% endhint %}

### New Player Experience

Think of your achievements like a meta quest ...&#x20;

{% hint style="info" %}
Meta means beyond or above, etc. and when we use it we mean a concept, information, etc. that is not part of the main but additional and external to it.
{% endhint %}

Like a meta quest, that is a quest for the player (not the character in-game world) to learn your game. To encourage them to explore the features and functions of your game in a structured manner and to offer some non-gameplay impacting rewards for doing so.

For a practical example of this see DOTA 2's "New Player Experience" aka "Welcome Quests" where they present "quests" for new players to do simple things like open menus, use features, review information, play each of the game modes, etc. Importantly this is not hidden from the player it's presented to the player in the menu just like a quest, showing what steps are yet to be done and which have been done.

{% embed url="https://www.youtube.com/watch?v=GtstEl0ULu4" %}
Not sponsored/promoted, this is just a random video on the topic of DOTA 2 Welcome Quests you might find relevant
{% endembed %}

### Player Tutorial

The best tutorials are fun and engaging parts of the game that happen to also teach the player mechanics, concepts, demonstrate tactics and strategies and more. Similar to the New Player Experience approach you can use Achievements as a means to draw attention to these instructions and reward their completion without forcing the player into them.

### Item Rewards

Steam Inventory is a huge topic unto itself that needs its own guide. The overlay with Achievements is that you can restrict eligibility for Item Promotion drops based on unlocked achievements. You can use this with New Player Experience or Tutorial style achievements to award in-game items for completing the tasks.

### Achievement Hunters

There are many types of players and a common one across all game genres is the "Collector" or "Hunter" This is a type of player that likes to "100%" the game. Be careful to not bloat your game with meaningless achievements as this will simply frustrate the collector but do make sure to track and reward them for fully exploring your game.

## Creating Achievements

> #### [Valve](https://partner.steamgames.com/doc/features/achievements)
>
> Steam Stats and Achievements provides an easy way for your game to provide persistent, roaming achievement and statistics tracking for your users. The user's data is associated with their Steam account, and each user's achievements and statistics can be formatted and displayed in their Steam Community Profile.

Achievements like stats are created in your [Steam Developer Portal](https://partner.steamgames.com/), once created there you can access them via their ID, if you're use Heathen's Steamworks ... why aren't you it has a free version. Then you can import your Stats and Achievements into Unity or use our [AchievementData ](../../heathens-steamworks-complete/unity/data-layer/achievement-data.md)structure to easily work with your achievements in code.

Valve's documentation on the [Stats and Achievement](https://partner.steamgames.com/doc/features/achievements) features is a good place to get started.
