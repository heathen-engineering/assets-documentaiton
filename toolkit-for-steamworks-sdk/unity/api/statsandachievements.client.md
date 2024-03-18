---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# StatsAndAchievements.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using StatsClient = HeathenEngineering.SteamworksIntegration.API.StatsAndAchievements.Client;
```

```csharp
public static class StatsAndAchievements.Client
```

All features available to 1 are present in the other with some minor exceptions. The only notable difference is that Server related calls required you to provide the CSteamID of the user to be adjusted and will only work when that user is authenticated to the Steam Game Server that calls the method.

### What can it do?

Set and reset Steam Stats and Achievements. Most of the features of the StatsAndAchievments interface can be accessed through its related objects.

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/avg-rate-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/float-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/int-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/achievement-object" %}



## Events

### EventUserStatsReceived

Called when the latest stats and achievements for a specific user (including the local user) have been received from the server.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(UserStatsReceived_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.StatsAndAchievement.Client.EventUserStatsReceived.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.StatsAndAchievement.Client.EventUserStatsReceived.RemoveListener(HandleEvent);
}
```

### EventUserStatsUnloaded

Callback indicating that a user's stats have been unloaded.

Assuming a handler in the form of

```csharp
private void HandleEvent(UserStatsUnloaded_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.StatsAndAchievement.Client.EventUserStatsUnloaded.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.StatsAndAchievement.Client.EventUserStatsUnloaded.RemoveListener(HandleEvent);
}
```

### EventUserStatsStored

Callback indicating that a user's stats have been stored.

Assuming a handler in the form of

```csharp
private void HandleEvent(UserStatsStored_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.StatsAndAchievement.Client.EventUserStatsStored.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.StatsAndAchievement.Client.EventUserStatsStored.RemoveListener(HandleEvent);
}
```

### EventUserAchievementStored

Callback indicating that a user's achievements have been stored.

Assuming a handler in the form of

```csharp
private void HandleEvent(UserAchievementStored_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.StatsAndAchievement.Client.EventUserAchievementStored.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.StatsAndAchievement.Client.EventUserAchievementStored.RemoveListener(HandleEvent);
}
```

## Methods

### ClearAchievement

```csharp
public static bool ClearAchievement(string achievementApiName)
```

Resets the achievement unlock state.

### GetAchievement

```csharp
public static bool GetAchievement(string achievementApiName, out bool achieved, out DateTime unlockTime)
```

or

```csharp
public static bool GetAchievement(CSteamID userId, string achievementApiName, out bool achieved)
```

or

```csharp
public static bool GetAchievement(CSteamID userId, string achievementApiName, out bool achieved, out DateTime unlockTime)
```

Gets the achievement status and date the achievement was unlocked if at all. This can be done for the local player or for a specific player by providing the player's ID

### GetAchievementAchievedPercent

```csharp
public static bool GetAchievementAchievedPercent(string achievementApiName, 
                                                 out float percent)
```

Returns the percentage of users who have unlocked the specified achievement

### GetAchievementDisplayAttribute

```csharp
public static string GetAchievementDisplayAttribute(string achievementApiName, 
                                AchievementAttributes attribute)
```

Get general attributes for an achievement. Currently provides Name, Description and Hidden status

### GetAchievementIcon

```csharp
public static void GetAchievementIcon(string achievementApiName, 
                                Action<Texture2D> callback)
```

Gets the icon for an achievement

The callback would take the form of

```csharp
void Callback(Texture2D icon)
{
    //DO WORK
}
```

### GetAchievementName

```csharp
public static string GetAchievementName(uint index)
```

Get the API Name for an achievement index between 0 and [GetNumAchievements](statsandachievements.client.md#getnumachievements)

### GetAchievementNames

```csharp
public static string[] GetAchievementNames()
```

Get a list of all achievement names registered to the app

### GetGlobalStat

```csharp
public static bool GetGlobalStat(string statApiName, out long data)
```

or

```csharp
public static bool GetGlobalStat(string statApiName, out double data)
```

Gets the lifetime total for an aggregated stat

### GetMostAchievedAchievements

```csharp
public static void GetMostAchievedAchievements(Action<EResult, (AchievementObject achievement, float percentage)[], bool> callback)
```

Gets a collection of the "most achieved achievements" this is a collection sorted by the statistically most achieved achievements for the game globally. The first entry will be the most achieved achievement globally with the last entry being the least.

The callback for this should take the following form

```csharp
void Callback(EResult result, (AchievementObject achievement, float percentage)[] data, bool IOError)
{
    if(result = EResult.k_EResultOK)
    {
        foreach(var entry in data)
        {
            Debug.Log($"{entry.achievement.name} has been achieved by {entry.percentage} of players");
        }
    }
}
```

### GetMostAchievedAchievementInfo

```csharp
public static int GetNextMostAchievedAchievementInfo(int previousIndex, 
                                out string achievementApiName, 
                                out float percent, 
                                out bool achieved)
```

Gets the info on the next most achieved achievement for the game.

You must have called RequestGlobalAchievementPercentages and it needs to return successfully via its callback prior to calling this.

* previousIndex\
  Iterator returned from the previous call to this method or from GetMostAchievedAchievementInfo
* achievementApiName\
  will be populated with the achievement name
* percent\
  will be populated with the percentage of people that have achieved this&#x20;
* achieved\
  true if the current user has this achievement unlocked

### GetNumAchievements

```csharp
public static uint GetNumAchievements()
```

Get the number of achievements defined in the App Admin panel of the Steamworks web site.

### GetNumberOfCurrentPlayers

```csharp
public static void GetNumberOfCurrentPlayers(Action<NumberOfCurrentPlayers_t, bool> callback)
```

Asynchronously retrieves the total number of players currently playing the current game. Both online and in offline mode.

The callback would take the form of

```csharp
void Callback(NumberOfCurrentPlayers_t result, bool IOError)
{
    //DO WORK
}
```

### GetStat

```csharp
public static bool GetStat(string statApiName, out int data)
```

or

```csharp
public static bool GetStat(string statApiName, out float data)
```

or

```csharp
public static bool GetStat(CSteamID userId, string statApiName, out int data)
```

or

```csharp
public static bool GetStat(CSteamID userId, string statApiName, out float data)
```

Gets the current value of the stat, optionally you can provide a user for whom you would like to get the stat of.

### IndicateAchievementProgress

```csharp
public static bool IndicateAchievementProgress(string achievementApiName, 
                                uint progress, 
                                uint maxProgress)
```

Shows the user a pop-up notification with the current progress of an achievement.

Calling this function will NOT set the progress or unlock the achievement, the game must do that manually by calling SetStat!

### RequestCurrentStats

```csharp
public static bool RequestCurrentStats()
```

Asynchronously request the user's current stats and achievements from the server.

You must always call this first to get the initial status of stats and achievements. Only after the resulting callback comes back can you start calling the rest of the stats and achievement functions for the current user.

{% hint style="warning" %}
When we initialize the Steam API for you via our Steamworks Behaviour will will call this for you. You shouldn't ever need to call this your self.
{% endhint %}

### RequestGlobalAchievementPercentages

```csharp
public static void RequestGlobalAchievementPercentages(Action<GlobalAchievementPercentagesReady_t, bool> callback)
```

Asynchronously fetch the data for the percentage of players who have received each achievement for the current game globally.

```csharp
void Callback(GlobalAchievementPercentageReady_t result, bool IOError)
{
    //DO WORK
}
```

### RequestGlobalStats

```csharp
public static void RequestGlobalStats(int historyDays, 
                                Action<GlobalStatsReceived_t, bool> callback)
```

Asynchronously fetches global stats data, which is available for stats marked as "aggregated" in the App Admin panel of the Steamworks website.

The callback for this method should take the form&#x20;

```csharp
void Callback(GlobgalStatsReceived_t results, bool IOError)
{
    //DO WORK
}
```

### RequestUserStats

```csharp
public static void RequestUserStats(CSteamID userId, 
                                Action<UserStatsReceived_t, bool> callback)
```

Asynchronously downloads stats and achievements for the specified user from the server.

To keep from using too much memory, an least recently used cache (LRU) is maintained and other user's stats will occasionally be unloaded. When this happens a UserStatsUnloaded\_t callback is sent. After receiving this callback the user's stats will be unavailable until this function is called again.

The callback for this method should take the form

```csharp
void Callback(UserStatsReceived_t results, bool IOError)
{
    //DO WORK
} 
```

### ResetAllStats

```csharp
public static bool ResetAllStats(bool achievementsToo)
```

Resets all stats, if you pass `true` in on the achievementToo parameter then it will also reset all achievements.

### SetAchievement

```csharp
public static bool SetAchievement(string achievementApiName)
```

Unlocks the achievement identified

### SetStat

```csharp
public static bool SetStat(string statApiName, int data)
```

or

```csharp
public static bool SetStat(string statApiName, float data)
```

Sets / updates the value of a given stat for the current user.

* statApiName\
  The `API Name` of the stat. Must not be longer than k\_cchStatNameMax.
* data\
  The new value of the stat. This must be an absolute value. it will not increment or decrement for you!

### StoreStats

```csharp
public static bool StoreStats()
```

Send the changed stats and achievements data to the server for permanent storage.

If this fails then nothing is sent to the server. It's advisable to keep trying until the call is successful. This call can be rate limited. Call frequency should be on the order of minutes, rather than seconds. You should only be calling this during major state changes such as the end of a round, the map changing, or the user leaving a server. This call is required to display the achievement unlock notification dialog though, so if you have called SetAchievement then it's advisable to call this soon after that.

### UpdateAvgRateStat

```csharp
public static bool UpdateAvgRateStat(string statApiName, 
                float countThisSession, 
                double sessionLength)
```

Updates an AVGRATE stat with new values.

* statApiName\
  The 'API Name' of the stat. Must not be longer than k\_cchStatNameMax.
* countThisSession\
  The value accumulation since the last call to this function.
* sessionLength\
  The amount of time in seconds since the last call to this function.

## How To

### Clear Achievements and Stats

You can clear achievements either by using the interface

```csharp
API.StatsAndAchievements.Client.ClearAChievement(name);
```

or by using the [Achievement Object](../classes-and-structs/achievement-object.md) directly

Resetting a stat is as simple as setting its value, see the [Int Stat](../classes-and-structs/int-stat.md) and [Float Stat](../classes-and-structs/float-stat.md) object for details

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

