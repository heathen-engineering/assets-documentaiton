---
description: Understanding Steam Achievements and the Heathen Engineering tool kit
---

# 🏆 Achievements

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

{% hint style="info" %}
The above link and repeated below so you can find it:\
[https://partner.steamgames.com/doc/features/achievements](https://partner.steamgames.com/doc/features/achievements)\
\
Is highly important, you should fully read Valve's own documentation around Steam Achievements to fully understand them. Some of the information will be summarized here in and notes on the tools and systems Heathen has created around Steam Achievements is documented below.&#x20;
{% endhint %}

> #### [Valve](https://partner.steamgames.com/doc/features/achievements)
>
> Steam Stats and Achievements provides an easy way for your game to provide persistent, roaming achievement and statistics tracking for your users. The user's data is associated with their Steam account, and each user's achievements and statistics can be formatted and displayed in their Steam Community Profile.

Heathen's Steamworks represents your defined Steam Achievements as scriptable objects associated with the [Steam Settings](../../../assets/steamworks/unity/scriptable-objects/steam-settings/). This allows your unity scripts to reference the achievements as you would any other Unity object e.g. by drag and drop and allows you to perform actions against a given achievement such as to unlock it by calling simple methods on that object.

## [API](../../../assets/steamworks/api/stats-and-achievements.md)

Heathen's Steamworks wraps Valve's Steam API with a C# and Unity friendly tool kit. All features related to stats and achievements can be found in the [StatsAndAchievements.Client](../../../assets/steamworks/api/stats-and-achievements.md) class. In most cases you wont need to use this low level tool but it is available to you and works very similar to the raw Steam API.

## [Achievement Data](../../../assets/steamworks/data-layer/achievement-data.md)

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

## [Achievement Object](../../../assets/steamworks/unity/scriptable-objects/achievement-object.md)

Heathen's Steamworks can "import" your achievements from Steam API directly and construct Scriptable Objects that makes it possible to work with achievements with zero coding required.

![](<../../../.gitbook/assets/image (176) (1) (1) (1) (1).png>)

Right from the Steam Settings object you import all of the Steam Achievements you defined in Valve's Steam Developer Portal.

{% hint style="info" %}
You must have the simulation running so the Steam API is initialized and able to talk to Steam client.
{% endhint %}

Once done you can find Scriptable Objects for each of the identified achievements nested under your Steam Settings

![](<../../../.gitbook/assets/image (167) (1) (1) (1) (1) (1) (1) (1) (1).png>)

You can learn more about the [Achievement Object](../../../assets/steamworks/unity/scriptable-objects/achievement-object.md) in our documentation. Using this object you can reference this achievement in any of your own logic and easily test for unlock and unlock the achievement.
