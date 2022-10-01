# StatsAndAchievements.Client

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using StatsClient = HeathenEngineering.SteamworksIntegration.API.StatsAndAchievements.Client;
```

```csharp
public static class StatsAndAchievements.Client
```

All features available to 1 are present in the other with some minor exceptions. The only notable difference is that Server related calls required you to provide the CSteamID of the user to be adjusted and will only work when that user is authenticated to the Steam Game Server that calls the method.

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

You can clear achievements either by using the interface

```csharp
API.StatsAndAchievements.Client.ClearAChievement(name);
```

or by using the [Achievement Object](../objects/achievement-object.md) directly

Resetting a stat is as simple as setting its value, see the [Int Stat](../objects/int-stat.md) and [Float Stat](../objects/float-stat.md) object for details

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

