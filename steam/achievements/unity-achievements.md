---
cover: ../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Unity Achievements

## Introduction

Once your achievements are defined and published in Steam Developer Portal you can start using them. You have 3 options with how you choose to engage with achievements or any other Steam "artefact" like it.

#### Object

We have defined Scriptable Objects for every major artefact type, these make it easy to reference your achievements in-game objects. The [Using Object References](unity-achievements.md#using-object-references) section of this article gives more detail.

#### Data Layer

We have defined C# structs for every major artefact type, these are suitable for DOTS and similar paradigms and do not require a reference at all. The [Using Value Types](unity-achievements.md#using-value-types) section of this article gives more detail.

#### API Extensions

We have wrapped every API endpoint, callback and feature in an engine-specific static class for cases where you prefer to work with an API directly. The [Using Heathen APIs](unity-achievements.md#using-heathen-apis) section of this article gives more detail.

## Using Achievements

The first thing to understand is that with stats and achievements, the process of setting them in two steps.

1. You assign the value such as `myAch.IsAchieved = true;`
2. You store the changes to the backend such as `myAch.Store()`

The notification popup will not trigger until the achievement is "stored". In the above examples "myAch" would be either an [AchievementObject ](../../heathens-steamworks-complete/unity/scriptable-objects/achievement-object.md)or [AchievementData](../../heathens-steamworks-complete/unity/data-layer/achievement-data.md), both do the same thing, "Object" is a reference type based on ScriptableObject so can be easily referenced in Unity Editor while "Data" is a value type e.g. a C# struct and more suitable for DOTS and related structures.

### Storing Achievements

This is the process of committing any changes made during gameplay to the Steam backend. That is you can freely "set" the state of achievements and stats during gameplay such as incrementing kills of enemy units, player score, etc. These changes are written to the local cash, not directly to the backend.

When the game is closed or when you call "Store" the changes will be committed to the backend. This should be done at key points in the game such as at the end of a level, on player death, when a boss is defeated or at some other opportune time. It is generally not recommended that you constantly call Store() with each change.

{% hint style="warning" %}
Think about when you want that popup to show\
It will be immersion-breaking, it could cover parts of the screen, and it could cause things such as Windows Auto HDR to cause screen flicker ... in generally you want it to show only when the player is not actively engaged in gameplay such as on a menu, debriefing, "You Died" screen, etc.
{% endhint %}

There are several ways to store stats and achievements and they all do the same thing. They are simply different ways you can trigger the effect depending on what objects you have available in memory and how you are more comfortable as a developer.

#### AchievementData

Assuming you have a data object named myAch

```csharp
myAch.Store();
```

#### AchievementObject

Assuming you have an object named myAch

```csharp
myAch.Store();
```

#### API

```csharp
API.StatsAndAchievements.Client.StoreStats();
```

### Pop up

The Steam popup that you're used to seeing when you unlock an achievement or receive some other notification is not code in the game but rather the Steam client rendering overtop the game's window.&#x20;

{% hint style="info" %}
Players can force this to be disabled so do not assume it will always be present it's the user's choice as configured in the Steam client, not your game. This is not for you to control.
{% endhint %}

For achievements, this popup triggers when an achievement is [stored ](unity-achievements.md#storing-achievements)not when it is set. Also, note that because it is rendering over the game window it will not likely work properly when testing in the Unity Editor or if you have a debugger or other app mounted to the process as this may restrict window updates and or add additional windows to the process.

### Using Value Types

[Achievement Data](../../heathens-steamworks-complete/unity/data-layer/achievement-data.md)

Heathen's Steamworks' Achievement Data simplifies working with Steam achievements exposing common features to a simple struct.

```csharp
//The achievement data struct is implicitly convertible from the string
//so you can convert the API name as a string into the data struct
AchievementData myAch = "achievement_API_name";

//You can understand the state of an achievement with simple fields
if(myAch.IsAchieved)
    Debug.Log($"{UserData.Me.Name} achieved this on {myAch.UnlockTime}");
else
    Debug.Log($"This has not been unlocked yet");

//You can unlock an achievement simply by assigning the IsAchieved value
myAch.IsAchieved = true;
```

### Using Object References

[Achievement Object](../../heathens-steamworks-complete/unity/scriptable-objects/achievement-object.md)

Heathen's Steamworks can "import" your achievements from Steam API directly and construct Scriptable Objects that make it possible to work with achievements with zero coding required.

![](<../../.gitbook/assets/image (176) (1) (1) (1) (1).png>)

Right from the Steam Settings object you import all of the Steam Achievements you defined in Valve's Steam Developer Portal.

{% hint style="info" %}
You must have the simulation running so the Steam API is initialized and able to talk to the Steam client.
{% endhint %}

Once done you can find Scriptable Objects for each of the identified achievements nested under your Steam Settings

![](<../../.gitbook/assets/image (167) (1) (1) (1) (1) (1) (1) (1) (1).png>)

You can learn more about the [Achievement Object](../../heathens-steamworks-complete/unity/scriptable-objects/achievement-object.md) in our documentation. Using this object you can reference this achievement in any of your logic and easily test for unlock and unlock the achievement.

```csharp
using UnityEngine;
using HeathenEngineering.SteamworksIntegration;

public class ExampleScript : MonoBehaviour
{
  public AchievementObject myAchievement;
  
  void Start()
  {
    if(myAchievement.IsAchieved)
      Debug.Log("It is unlocked");
    else
      Debug.Log("It is locked");
  }
}
```

### Using Heathen APIs

[API](../../heathens-steamworks-complete/unity/api/statsandachievements.client.md)

Heathen's Steamworks wraps Valve's Steam API with a C# and Unity-friendly tool kit. All features related to stats and achievements can be found in the [StatsAndAchievements.Client](../../heathens-steamworks-complete/unity/api/statsandachievements.client.md) class. In most cases, you won't need to use this low-level tool but it is available to you and works very similar to the raw Steam API.

```csharp
using UnityEngine;
using Achievements = HeathenEngineering.SteamworksIntegration.API.StatsAndAchievements.Client;

public class ExampleScript : MonoBehaviour
{
  void Start()
  {
    Achievements.GetAchievement("ACH_TRAVEL_FAR_ACCUM", out bool isAchieved);
    
    if(isAchieved)
      Debug.Log("It is unlocked");
    else
      Debug.Log("It is locked");
      
    //To unlock it
    Achievements.SetAchievement("ACH_TRAVEL_FAR_ACCUM");
    
    //To re-lock it
    Achievements.ClearAchievement("ACH_TRAVEL_FAR_ACCUM");
  }
}
```
