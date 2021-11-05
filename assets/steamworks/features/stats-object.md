---
description: Understanding Steam Stats and the Heathen Engineering tool kit
---

# Stats

{% embed url="https://www.youtube.com/watch?v=Mcjzox4e-js&list=PL2R4tvBs-r1ncN8Y7SoF5IX-WY6K2m9AT&index=4" %}

{% hint style="warning" %}
Please note that you must call StoreStatsAndAchievements to apply changes to the Steam backend, and thus cause the notification to pop up.

```csharp
SteamSettings.Client.StoreStatsAndAchievements();
```
{% endhint %}

## Creating a Stat

Stats objects are created on the [`SteamSettings`](steam-settings.md#stats-object) object. To learn more please read the documentation on [Steam Settings](steam-settings.md#stats-object).

{% hint style="info" %}
Steam stat objects can be used to upload stat values to the Steam Backend. You can read more about the Steam Stats system here [https://partner.steamgames.com/doc/features/achievements](https://partner.steamgames.com/doc/features/achievements)
{% endhint %}

## Examples

### Upload Value (Client)

All stat objects have a data type being either a `FloatStatObject` or an `IntStatObject` in all cases you can set the value via the `Value` member.

Note this will only work if the stat in question is configured fro "Set By" = "Client"

```csharp
stat.Value = 42;
//or
stat.Value = 42.5f;
```

### Get Value (Client)

The `Value` member of the `FloatStatObject` or `IntStatObject` can be used to access its current value.

Note this will only work if the stat in question is configured fro "Set By" = "Client"

```csharp
var valueIs = stat.Value;
```

### Upload Value (Server)

For servers the user isn't known ahead of time, so you must provide the user to be updated for.

```csharp
//For a float stat use
stat.SetUserFloatStat(userId, 42.5f);
//For an int stat use
stat.SetUserIntStat(userId, 42);
```

### Get Value (Server)

For servers the user isn't known ahead of time, so you must provide the user to be updated for.

```csharp
//For a float stat use
var value = stat.GetUserFloatStat(userId);
//For an int stat use
var value = stat.GetUserIntStat(userId);
```
