---
description: Understanding Steam Achievements and the Heathen Engineering tool kit
---

# Achievements

## Introduction

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

Heathen's Steamworks represents yoru defined Steam Achievements as scriptable objects assoceatted with the [Steam Settings](steam-settings.md). This allows your unity scripts to reference the achievements as you would any other Unity object e.g. by drag and drop and allows you to perform actions against a given achievement such as to unlock it by calling simple methods on that object.

### Tutorial Videos

{% embed url="https://www.youtube.com/watch?v=Mcjzox4e-js&list=PL2R4tvBs-r1ncN8Y7SoF5IX-WY6K2m9AT&index=4" %}

{% hint style="warning" %}
Please note that you must call StoreStatsAndAchievements to apply changes to the Steam backend and thus cause the notification to pop up.

```csharp
SteamSettings.Client.StoreStatsAndAchievements();
```
{% endhint %}

## Creating an Achievement

This assumes you have already created the achievement in the Steam developer portal as outlined in [Valve's documentaiton](https://partner.steamgames.com/doc/features/achievements). Once done you will need to create a reference to the achievement in the Steam Settings as shown below

![](<../../../.gitbook/assets/image (149).png>)

When you create a new AchievmentObject you will need to provide it with an Achievment Name, this is the API name of the achievement as it appears in your Steam Developer Portal.

![Screen shot of Steam's developer portal when creating an achievement ... this shows the name you need](<../../../.gitbook/assets/image (27).png>)

![Screen shot of a new Achievement in the Steam Settings and the field where you should place the name](<../../../.gitbook/assets/image (150).png>)

{% hint style="info" %}
&#x20;Steam achievement objects can be used to recognize key events in your app. You can read more about the Steam Stats system here [https://partner.steamgames.com/doc/features/achievements](https://partner.steamgames.com/doc/features/achievements)
{% endhint %}

## Examples

&#x20;These examples assume you have a reference to your achievment object named `achievement`. To create such a reference, you can do the following any mono behavior and simply drag a reference to it in the Unity inspector.

### Reference an achievement

This assumes you will drag the desired achievement onto the inspector of this script into this field.

```csharp
public AchievementObject achievement;
```

### Find achievement by name

This assumes you are comfortable using linq and know that the `"id of achievement"` should be replaced with the actual ID of your achievement.

```csharp
achievement = SteamSettings.Achievements.FirstOrDefault
    (p => p.achievementId == "id of achievement");
```

### Unlock the achievement

```csharp
achievement.Unlock();
```

### Clear / Reset achievement

```csharp
achievement.ClearAchievement();
```

### Check if achieved/unlocked

```csharp
if(achievement.isAchieved)
  Debug.Log("It is achieved / unlocked");
```

### UnityEvent on Unlocked

```csharp
achievement.OnUnlock.AddListener(HandleUnlockOfAchievement);
```

then you should have a method such as

```csharp
private void HandleUnlockOfAchievement()
{
  Debug.Log("The achievement was unlocked / achieved");
}
```

{% hint style="warning" %}
You can only set achievements that are configured on the Steam Portal to allow "Set By" client. You can read more about Stats in [Valve's own documentation](https://partner.steamgames.com/doc/features/achievements).
{% endhint %}
