# StatsAndAchievements.Server



{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

```csharp
using StatsServer = HeathenEngineering.SteamworksIntegration.API.StatsAndAchievements.Server;
```

```csharp
public static class StatsAndAchievements.Server
```

All features available to 1 are present in the other with some minor exceptions. The only notable difference is that Server related calls required you to provide the CSteamID of the user to be adjusted and will only work when that user is authenticated to the Steam Game Server that calls the method.

### What can it do?

Set and reset Steam Stats and Achievements. Most of the features of the StatsAndAchievments interface can be accessed through its related objects.

### Related Obejcts

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/avg-rate-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/float-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/int-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/achievement-object" %}
