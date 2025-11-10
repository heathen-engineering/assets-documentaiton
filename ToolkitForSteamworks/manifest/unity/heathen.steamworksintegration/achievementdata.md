---
description: public struct AchievementData
---

# AchievementData

Represents a Steam Achievement

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

### Scriptable Object

```csharp
public AchievementObject ScriptableObject { get; set; }
```

The ScriptableObject representation of this Achievement if one exists and is registered to the active Heathen.SteamworksIntegration.SteamSettings object

***

### Unlock Time

```csharp
public System.DateTime? UnlockTime { get; }
```

Indicates the time the achievement was unlocked if at all

***

## Funcitons

### Clear Achievement

```csharp
public void ClearAchievement();
// or
public void ClearAchievement(UserData user);
```

Resets the unlock status of an achievement or clears the achievement for the user.

***

### Compare To

```csharp
public int CompareTo(AchievementData other);
// or
public int CompareTo(string other);
```

Compares one achievement to another or to a string for the API name; this is an IComparable member.

***

### Create ScriptableObject

```csharp
public AchievementObject CreateScriptableObject();
// or
public static AchievementObject CreateScriptableObject(string apiName);
```

This will create a ScriptableObject ... in general, you should not need this. The AchievementData struct has all the same features of the ScriptableObject but is much lighter weight and more suitable for creation at runtime.

***

### Equals

```csharp
public bool Equals(AchievementData other);
// or
public override bool Equals(object obj);
// or
public bool Equals(string other);
```

True if the input equates to the AchievementData value as this. For object, we will try for a cast to AchievementData or string and for string, we check the API name.

***

### Get

```csharp
public static AchievementData Get(string apiName);
```

Get the achievement given the API name provided

***

### Get Achievement and Unlock time

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

### Get Hash Code

```csharp
public override int GetHashCode();
```

Returns a hash code value for this object

***

### Get Icon

```csharp
public void GetIcon(Action<Texture2D> callback);
```

Gets the icon for this achievement as seen by the logged-in user; this will return either the locked or unlocked icon, depending on the state of the achievement for this user

***

### Store

```csharp
public void Store();
```

Request Steam client store the current state of all stats and achievements

***

### To String

```csharp
public override string ToString();
```

Returns the API Name of the achievement

***

### Unlock

```csharp
public void Unlock();
// or
public void Unlock(UserData user);
```

Unlocks the achievement for this user, or for game servers you can provide the user to unlock for. Note, you can only unlock for an achievement that is set to GS or GS Official, and only after authenticating the user and requesting that user's stats.

***

## Operators

### Assignment

```csharp
public static implicit operator AchievementData(string id);
// or 
public static implicit operator string(AchievementData value);
```

Allows you to set an AchievementData from a string, or a string from an AchievementData.

***

### Equality

```csharp
public static bool operator !=(AchievementData l, AchievementData r)
// or
public static bool operator !=(AchievementData l, string r)
// or
public static bool operator !=(string l, AchievementData r)
// or
public static bool operator ==(AchievementData l, AchievementData r)
// or 
public static bool operator ==(AchievementData l, string r)
// or
public static bool operator ==(string l, AchievementData r)
```

Allows you to compare AchievementData and string values for equality.

***
