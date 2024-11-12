---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Achievement Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

<pre class="language-csharp"><code class="lang-csharp"><strong>using HeathenEngineering.SteamworksIntegration;
</strong></code></pre>

```csharp
public struct AchievementData : IEquatable<AchievementData>, 
                                IEquatable<string>, 
                                IComparable<AchievementData>, 
                                IComparable<string>
```

A data wrapper around Steam's concept of an Achievement. This is implicitly convertible from string expecting that string to be the "API Name" of the achievement.

```csharp
AchievementData myAch = "ACH_WIN_100_GAMES";
myAch.IsAchievd = true;
myAch.Store();
```

Achievements are a common feature of Steam API and one of the simpler to implement. They are typically used to mark milestones or key accomplishments of the player, you can learn more in our [Steam Guides](../../../steam/achievements.md).

## Fields and Attributes

### Name

```csharp
public string Name => get;
```

Returns the display name of this achievement if defined.

### Description

```csharp
public string Description => get;
```

The description of this achievement if defined.

### Hidden

```csharp
public bool Hidden => get;
```

Returns the display attribute "hidden" for this achievement.

### IsAchieved

```csharp
public bool IsAchieved { get; set; }
```

Is the achievement "unlocked" ... this can only be set if the achievement is set to allow client write. If set to GS or Trusted write only then the attempt to set it will be ignored.

### UnlockTime

```csharp
public DateTime? UnlockTime => get;
```

The time this achievement was achieved... if any, this can be null

### GlobalPercent

```csharp
public float GlobalPercent => get;
```

The percentage of users who have unlocked this achievement

## Methods

### Unlock

```csharp
public void Unlock()
```

The same as assigning true to the IsAcheived field.

```csharp
public void Unlock(UserData user)
```

Only used on servers, this can be used to unlock the achievement for a specific user.

### ClearAchievement

```csharp
public void ClearAchievement()
```

The same as assigning false to the IsAcheived field.

```csharp
public void ClearAchievement(UserData user)
```

Only used on servers, this can be used to clear / lock the achievement for a specific user.

### GetAchievementStatus

```csharp
public bool GetAchievementStatus(UserData user)
```

Gets the status (locked/unlocked) for the given user. This is only used on server builds.

### GetAchievementAndUnlockTime

```csharp
public (bool unlocked, DateTime unlockTime) GetAchievementAndUnlockTime(UserData user)
```

Gets the unlock status and the time the user unlocked it if any. This is only used on server builds.

This uses a tuple which is a standard feature of C#, you can learn more about it here

{% embed url="https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples" %}

### GetIcon

```csharp
public void GetIcon(Action<Texture2D> callback)
```

Returns the icond for the user based on the user's current state. That is if the user has this achievement unlocked then the unlocked image will be returned, else if not the locked image will be returned.

### Store

```csharp
public void Store()
```

A simple short cut to the Stats and Achievements Store Stats and achievements. You can call this on any achievement or stat and it will commit all changes to the backend for all stats and achievements.
