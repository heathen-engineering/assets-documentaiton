---
description: Be better than "killed 10 rats"
---

# 🏆 Achievements

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Achievements are a simple and traditional feature for games that can help drive player engagement. While they are simple to implement (make work) coming up with a good achievement design is not so simple. You could of course :face\_vomiting: forth random achievements like "Played 15 min", "Logged into the game", "Pressed the space bar"; but these are often time harmful to the game not helpful.

First understand that not every game needs achievements, that if your going to have achievements that they should be part of the game and not an after thought you bolted on because why not. Meaningless achievements can harm the user experience by breaking immersion or simply drawing attention away during gameplay.

Follows are some ideas for meaningful achievements and how you might tie those achievements into other aspects of your game.

## New Player Experience

Think of your achievements like a meta quest ...&#x20;

{% hint style="info" %}
Meta means beyond or above, etc. and when we use it we mean a concept, information, etc. that is not part of the main but additional and external to it.
{% endhint %}

Like a meta quest, that is a quest for the player (not the character in game world) to learn your game. To encourage them to explore the features and functions of your game in a structured manner and to offer some non-gameplay impacting reward for doing so.

For a practical example of this see DOTA 2's "New Player Experience" aka "Welcome Quests" where they present "quests" for new players to do simple things like open menus, use features, review information, play each of the game modes, etc. Importantly this is not hidden from the player its presented to the player in the menu's just like a quest, showing what steps are yet to be done and which have been done.

{% embed url="https://www.youtube.com/watch?v=GtstEl0ULu4" %}
Not sponsored / promoted, this is just a random video on the topic of DOTA 2 Welcome Quests you might find relevant
{% endembed %}

## Tutorial

The best tutorials fun and engaging parts of the game that happen to also teach the player mechanics, concepts, demonstrate tactics and strategies and more. Similar to the New Player Experience approach you can use Achievements as a means to draw attention to these instructions and reward their completion without forcing the player into them.

## Item Rewards

Steam Inventory is a huge topic unto its self that needs its own guide. The overlay with Achievements is that you can restrict eligibility for Item Promotion drops based on unlocked achievements. You can use this with New Player Experience or Tutorial style achievements to award in-game items for completing the tasks.

## Collectors

There are many types of players and a common one across all game genres is the "Collector" this is a type of player that likes to "100%" the game. Be carful to not bloat your game with meaningless achievements as this will simply frustrate the collector but do make sure to track and reward them for fully exploring your game.

## Creating Achievements

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

> #### [Valve](https://partner.steamgames.com/doc/features/achievements)
>
> Steam Stats and Achievements provides an easy way for your game to provide persistent, roaming achievement and statistics tracking for your users. The user's data is associated with their Steam account, and each user's achievements and statistics can be formatted and displayed in their Steam Community Profile.

Achievements like stats are created in your [Steam Developer Portal](https://partner.steamgames.com/), once created there you can access them via their ID, if your use Heathen's Steamworks ... which why aren't you it has a free version. Then you can import your Stats and Achievements into Unity or use our AchievementData structure to easily work with your achievements in code.



Valve's own documentation on the [Stats and Achievement](https://partner.steamgames.com/doc/features/achievements) features is a good place to get started.

### Quick Start

Log into your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../../.gitbook/assets/image.png" alt="Techincal Tools"><figcaption></figcaption></figure>

From there select the Stats & Achievements > Achievements option and create your new achievements. Make note of the value you use in the API Name field. You will use it when working with achievements in code. In Unity if you prefer to work with Achievements via an object reference then you can use our AchievementObject which is a Unity ScriptableObject that can be referenced and accessed like any other Unity Object.

<figure><img src="../../.gitbook/assets/image (1).png" alt="Achievement test"><figcaption></figcaption></figure>

## Using Achievements

The first thing to understand is that with stats and achievements the process of setting them is two steps.

1. You assign the value such as `myAch.IsAchieved = true;`
2. You store the changes to the backend such as `myAch.Store()`

The notification popup will not trigger until the achievement is "stored"&#x20;

### Storing Achievements

This is the process of committing any changes made during gameplay to the Steam backend. That is you can freely "set" the state of achievements and stats during gameplay such as incrementing kills of enemy units, player score, etc. These changes are written to the local cash not directly to the backend.

When the game is closed or when you call "Store" the changes will be committed to the backend. This should be done at key points in the game such as at the end of a level, on player death, when a boss is defeated or at some other opportune time. It is generally not recommend that you constantly call Store with each change.

{% hint style="warning" %}
Think about when you want that popup to show\
It will be immersion breaking, it could cover parts of the screen, it could cause things such as Windows Auto HDR to cause screen flicker ... in generally you want it to show only when the player is not actively engaged in gameplay such as on a menu, debriefing, "You Died" screen, etc.
{% endhint %}

### Using Value Types

[Achievement Data](../../assets/steamworks/data-layer/achievement-data.md)

Heathen's Steamworks' Achievement Data simplifies working with Steam achievements exposing common features to a simple struct.

```csharp
//The achievement data struct is implictly convertable from string
//so you can convert the API name as a string into the data struct
AchievementData myAch = "achievement_API_name";

//You can understand the state of an achievement with simple fields
if(myAch.IsAchieved)
    Debug.Log($"{UserData.Me.Name} achieved this on {myAch.UnlockTime}");
else
    Debug.Log($"This has not been unlocked yet");

//You can unlock and achievement simply by assigning the IsAchieved value
myAch.IsAchieved = true;
```

### Using Object References

[Achievement Object](../../assets/steamworks/unity/scriptable-objects/achievement-object.md)

Heathen's Steamworks can "import" your achievements from Steam API directly and construct Scriptable Objects that makes it possible to work with achievements with zero coding required.

![](<../../.gitbook/assets/image (176) (1) (1) (1) (1).png>)

Right from the Steam Settings object you import all of the Steam Achievements you defined in Valve's Steam Developer Portal.

{% hint style="info" %}
You must have the simulation running so the Steam API is initialized and able to talk to Steam client.
{% endhint %}

Once done you can find Scriptable Objects for each of the identified achievements nested under your Steam Settings

![](<../../.gitbook/assets/image (167) (1) (1) (1) (1) (1) (1) (1) (1).png>)

You can learn more about the [Achievement Object](../../assets/steamworks/unity/scriptable-objects/achievement-object.md) in our documentation. Using this object you can reference this achievement in any of your own logic and easily test for unlock and unlock the achievement.

```csharp
using UnityEngine;
using HeathenEngineering.SteamworksIntegration;

public class ExampleScript : MonoBehaviour
{
  public AchievementObject myAchievement;
  
  void Start()
  {
    if(myAchievement.IsAchieved)
      Debug.Log("It is unlocked");
    else
      Debug.Log("It is locked");
  }
}
```

### Using Heathen APIs

[API](../../assets/steamworks/api/stats-and-achievements.md)

Heathen's Steamworks wraps Valve's Steam API with a C# and Unity friendly tool kit. All features related to stats and achievements can be found in the [StatsAndAchievements.Client](../../assets/steamworks/api/stats-and-achievements.md) class. In most cases you won't need to use this low level tool but it is available to you and works very similar to the raw Steam API.

```csharp
using UnityEngine;
using Achievements = HeathenEngineering.SteamworksIntegration.API.StatsAndAchievements.Client;

public class ExampleScript : MonoBehaviour
{
  void Start()
  {
    Achievements.GetAchievement("ACH_TRAVEL_FAR_ACCUM", out bool isAchieved);
    
    if(isAchieved)
      Debug.Log("It is unlocked");
    else
      Debug.Log("It is locked");
      
    //To unlock it
    Achievements.SetAchievement("ACH_TRAVEL_FAR_ACCUM");
    
    //To re-lockit
    Achievements.ClearAchievement("ACH_TRAVEL_FAR_ACCUM");
  }
}
```

## Pop up

The Steam popup that your used to seeing when you unlock and achievement or receive some other notification is not actually code in the game but rather the Steam client rendering overtop the game's window.&#x20;

{% hint style="info" %}
Players can force this to be disabled so do not assume it will always be present its user's choice as configured in Steam client not your game. This is not for you to control.
{% endhint %}

For achievements this popup triggers when an achievement is [stored ](achievements.md#storing-achievements)not when it is set.
