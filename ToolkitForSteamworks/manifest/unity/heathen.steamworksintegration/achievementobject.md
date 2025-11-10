---
description: 'public class AchievementObject : ScriptableObject'
---

# AchievementObject

A UnityEngine.ScriptableObject containing the definition of a Steamworks Achievement.

## Fields and Attributes

### Api Name

```csharp
public string ApiName { get; }
```

The unique ID of the achievement is the API Name that has been set in the Steamworks portal.

***

### Description

```csharp
public string Description { get; }
```

Returns the description of the achievement as seen by this user, which will depend on the user's language and the language configuration of the achievement

***

### Global Percent

```csharp
public float GlobalPercent { get; }
```

The percentage of users who have unlocked this achievement

***

### Hidden

```csharp
public bool Hidden { get; }
```

Returns the Is Hidden value of this achievement as seen by this user

***

### Is Achieved

```csharp
public bool IsAchieved { get; set; }
```

Indicates that this achievement has been unlocked by this user.

> Only available on client builds

***

### Name

```csharp
public string Name { get; }
```

Returns the name of the achievement as seen by this user; this will depend on the user's language and the language configuration of the achievement

***

### Unlock Time

```csharp
public System.DateTime? UnlockTime { get; }
```

Indicates the time the achievement was unlocked, if at all

***

## Funcitons

### Clear Achievement

```csharp
public void ClearAchievement();
// or
public void ClearAchievement(UserData user)
```

Resets the unlock status of an achievement. Only a Steam Game Server that has authenticated a user can clear an achievement for that user.

***

### Crete Scriptable Object

```csharp
public static AchievementObject CreateScriptableObject(string apiName);
```

This will create a ScriptableObject based on this achievement ... in general, you should not need this. The AchievementData struct has all the same features of the ScriptableObject but is much lighter weight and more suitable for creation at runtime.

***

### Get Achievement and Unlock Time

```csharp
public (bool unlocked, DateTime unlockTime) GetAchievementAndUnlockTime(UserData user);
```

Get the unlock state and time for this achievement for a specific user.

***

### Get Achievement Status

```csharp
public bool GetAchievementStatus(UserData user);
```

Gets the achievement status for the user

***

### Get Icon

```csharp
public void GetIcon(Action<Texture2D> callback);
```

Gets the icon for this achievement as seen by the logged in user, this will return either the locked or unlocked icon depending on the state of the achievement for this user.

***

### Store

```csharp
public void Store();
```

Request Steam client store the current state of all stats and achievements

***

### Unlock

```csharp
public void Unlock();
// or
public void Unlock(UserData user);
```

Unlock the achievement for the user

***
