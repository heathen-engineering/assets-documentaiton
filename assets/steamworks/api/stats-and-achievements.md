# Stats & Achievements

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

```csharp
public static class API.StatsAndAchievements
```

Client features are available under the client interface

```csharp
API.StatsAndAchievements.Client
```

Server features are available under the server interface

```csharp
API.StatsAndAchievements.Server
```

All features availabel to 1 are present in the other with some minor exceptions. The only notable difference is that Server related calls required you to provide the CSteamID of the user to be adjusted and will only work when that user is authenticated to the Steam Game Server that calls the method.

### What can it do?

Set and reset Steam Stats and Achievements. Most of the features of the StatsAndAchievments interface can be accessed through its related objects.

### Related Obejcts

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/avg-rate-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/float-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/int-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/achievement-object" %}



## Events

### User Stats Received

Called when the latest stats and achievements for a specific user (including the local user) have been received from the server.

### User Stats Unloaded

Callback indicating that a user's stats have been unloaded.

### User Stats Stored

Invoked when the user's stats are stored to Steam's backend

### User Achievement Stored

Invoked when the user's achievements are stored to Steam's backend

## How To

### Clear Achievements and Stats

You can clear achievemnts either by using the interface

```csharp
API.StatsAndAchievements.Client.ClearAChievement(name);
```

or by using the [Achievement Object](../objects/achievement-object.md) directly

Reseting a stat is as simple as setting its value, see the [Int Stat](../objects/int-stat.md) and [Float Stat](../objects/float-stat.md) object for details

You can optionally reset all stats and achievements

```csharp
API.StatsAndAchievements.Client.ResetAllStats(bool andAchievements);
```

### Set a Stat or Achievement

Its generally simplest to use the artifact object directly so the Achievement Object, Int Stat or Float Stat. You can also set them through the interface

```csharp
API.StatsAndAchievments.Client.SetStat(value);
```

```csharp
API.StatsAndAchievements.Client.SetAchievement(achievementName);
```
