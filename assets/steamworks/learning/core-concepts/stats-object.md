---
description: Understanding Steam Stats and the Heathen Engineering tool kit
---

# Stats

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

{% hint style="success" %}
WIP



This page will discribe the features and use of Steam APIs authentication tools and how might use that feature in practical sitautions.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=Mcjzox4e-js&list=PL2R4tvBs-r1ncN8Y7SoF5IX-WY6K2m9AT&index=4" %}

{% hint style="warning" %}
Please note that you must call StoreStatsAndAchievements to apply changes to the Steam backend, and thus cause the notification to pop up.

```csharp
SteamSettings.Client.StoreStatsAndAchievements();
```
{% endhint %}
