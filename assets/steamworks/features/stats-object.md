---
description: Understanding Steam Stats and the Heathen Engineering tool kit
---

# Stats

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

{% hint style="warning" %}
Please note that you must call StoreStatsAndAchievements to apply changes to the Steam backend, and thus cause the notification to pop up.

```csharp
API.StatsAndAchievements.Client.StoreStats();
```
{% endhint %}

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Creating Stats

Stats work much like achievements however they cannot be imported from Valve directly so you must add your stats to your system manually.

![](<../../../.gitbook/assets/image (188).png>)

Once you add a sate you need to provide its API name exactly as you created it in the Steam Developer Portal.

![](<../../../.gitbook/assets/image (160) (1).png>)

## Using Stats

See the [Int Stat Object](../objects/int-stat.md), [Float Stat Object](../objects/float-stat.md) and [Avg Rate Stat Object](../objects/avg-rate-stat.md) for details on how to use each. In general though the process is that you will create a reference to the stat in question in one of your game's scripts such as

```csharp
public IntStatObject myIntStat;
```

This will make a new reference slot you can drag and drop your stat into on the Unity inspector for that object.

![](<../../../.gitbook/assets/image (174).png>)

You can now drag the desired stat object from your Steam Setting into that slot.

![](<../../../.gitbook/assets/image (159).png>)

![](<../../../.gitbook/assets/image (161) (1) (1).png>)

Your script can now perform actions in relation to that stat

```csharp
// Read the stat value
Debug.Log("Value is " + myIntStat.Value);

// Set the stat value
myIntStat.Value = 42;

// Store the stat values (effects all stats)
myIntStat.StorStats();
```

