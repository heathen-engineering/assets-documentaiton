---
description: Understanding Steam Stats and the Heathen Engineering tool kit
---

# ⭐ Stats

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="warning" %}
Please note that you must call StoreStatsAndAchievements to apply changes to the Steam backend, and thus cause the notification to pop up.

```csharp
API.StatsAndAchievements.Client.StoreStats();
```
{% endhint %}

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Unity

### Creating Stats

Stats work much like achievements however they cannot be imported from Valve directly so you must add your stats to your system manually.

![](<../../../.gitbook/assets/image (188) (1) (1) (1).png>)

Once you add a sate you need to provide its API name exactly as you created it in the Steam Developer Portal.

![](<../../../.gitbook/assets/image (160) (1) (1).png>)

### Using Stats

See the [Int Stat Object](../../../toolkit-for-steamworks/unity/objects/classes/int-stat.md), [Float Stat Object](../../../toolkit-for-steamworks/unity/objects/classes/float-stat.md) and [Avg Rate Stat Object](../../../toolkit-for-steamworks/unity/objects/classes/avg-rate-stat.md) for details on how to use each. In general though the process is that you will create a reference to the stat in question in one of your game's scripts such as

```csharp
public IntStatObject myIntStat;
```

This will make a new reference slot you can drag and drop your stat into on the Unity inspector for that object.

![](<../../../.gitbook/assets/image (174) (1) (1) (1).png>)

You can now drag the desired stat object from your Steam Setting into that slot.

![](<../../../.gitbook/assets/image (159) (1) (1) (1).png>)

![](<../../../.gitbook/assets/image (161) (1) (1) (1) (1) (1).png>)

Your script can now perform actions in relation to that stat

```csharp
// Read the stat value
Debug.Log("Value is " + myIntStat.Value);

// Set the stat value
myIntStat.Value = 42;

// Store the stat values (effects all stats)
myIntStat.StorStats();
```

### Global Stats

#### From Value

> Stats can be marked as aggregated on the admin page to tell Steam to keep a global total of all users' values for the stat. This can be used to get data on total money in the economy, total kills, favorite weapons, favorite maps, and which team tends to do better. On the flip side, this should not be used for stats like "MostKills" as adding that up for multiple users would be meaningless. As stats are in the hands of users, this data is subject to being manipulated. Therefore it's crucial when using aggregated stats to set good bounds for min value, max value, increment only (if appropriate), and max change. Max change has a special meaning for aggregated stats. When a new value is uploaded, the global value will change no more than the max change value. This limits how quickly a cheater can influence the global totals.

To read global stats you need to first request them, this will read the current state of the global stats for the app optionally with a date range for the number of "day by day" values to read for.

#### [Request Global Stats](../../../toolkit-for-steamworks/unity/api-extensions/statsandachievements.client.md#requestglobalstats)

> How many days of day-by-day history to retrieve in addition to the overall totals. The limit is 60.

```csharp
StatsAndAchievements.Client.RequestGlobalStats(60, callback);
```

The callback will notify you when the stats are ready to be read.

#### [Get Global Stat](../../../toolkit-for-steamworks/unity/api-extensions/statsandachievements.client.md#getglobalstat)

you can read global stats as a long or a double, below is an example of reading a long value.

```csharp
if(StatsAndAchievements.Client.GetGlobalStat("statAPIName", out long value))
{
  ;//value is the value
}
else
{
  ;//did not read anything
}
```

## Unreal

### Creating Stats

You create your stats in the Steamworks Developer Portal, you work with stats via their "API Name"

{% hint style="warning" %}
Pay attention to the "Set By" value, if this is not set to "Client" then the game client will not be able to set the stat and you will need to work with Steam Game Server to write values to the stat. This is useful if you need the stat to be "secure" e.g. to prevent players from writing whatever value they want to the stat.
{% endhint %}

![](<../../../.gitbook/assets/image (160) (1) (1).png>)

### Using Stats

Steam user's can read and write their own stats (assuming Set By = Client)&#x20;

Steam Game Server's (your server build that initialized Steamworks SDK) can read and write (assuming Set By is not Client) the stats for any user authenticated against it and that it has requested stats for.

<figure><img src="../../../.gitbook/assets/image (418).png" alt=""><figcaption></figcaption></figure>

### Global Stats

In Unreal we handle the async nature of Global History stats at the time of call, the callback will invoke when the result is ready

<figure><img src="../../../.gitbook/assets/image (420).png" alt=""><figcaption></figcaption></figure>
