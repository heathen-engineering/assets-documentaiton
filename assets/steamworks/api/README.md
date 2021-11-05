---
description: The Heathen Steam API wrapper
---

# API

{% hint style="warning" %}
Coming Soon

This will be released with Patch 13 and is expected late 2021 to early 2022 as a free update to Steamworks V2
{% endhint %}

## Introduction

The Heathen API provides access to the full Steam API wrapping every interface with a Unity friendly static class, simplifying use of the raw API without reducing its funcitonality and exposing every callback as a UnityEvent and every callresult as a Unity firendly Action.

We have wrapped every interface (except Networking interfaces) and copied its relivent documentaiton meaning you can now explore Valve's own documentaiton in yoru IDE via intellisense, take full advantage of auto complete and sugestions and explore the full API via the object explorer.&#x20;

{% hint style="info" %}
Why not wrap the networking interfaces?

We feel networking is best served working directly against the API with no "middle layer" sitting between. We are happy to revisit this if there is a community demand for it.
{% endhint %}

### Is this just Facepunch from Heathen?

No

We are still built on top of Steamworks.NET something we feel strongly about as it provides an unadultrated view of the Steam API making it possible for you to leverage decades of community guides, sample code, the offical Steam Developer forums and support channels from Valve, etc.

Heathen's API does wrap the raw Steam API up as an extension to Steamworks.NET making it not just C# friendly but more Unity native. You could say what Facepunch does for a C# programmer Heathen does for a Unity programmer, Unity designer, C# programmer, C/C++ programmer, etc.

## Features

### Platform Smart

Every interface has been organized into subsclasses (.Client and .Server) making it clear what is available to the client, to a server or both. This works with conditional compile optionally stripping away code that is not available to the current build platform.

EXAMPLES

```csharp
//Clearly client only
API.StatsAndAchievements.Client.ClearAchievement(achievement);

//Clearly server only
API.StatsAndAchievements.Server.ClearUserAchievement(user, achievement);
```

### Simply C\#

Valve's Steam API is big, powerful and written in C and C++ ... not exsactly friendly to many of the tride and true patterns and structures we use in C#. Heathen's API still exploses the traditional methods but also provides C# based alternatives.

TRADITIONAL

```csharp
var count = API.StatsAndAchievements.Client.GetNumAchievements();
var results = new string[count];
for (int i = 0; i < count; i++)
{
    results[i] = API.StatsAndAchievements.Client.GetAchievementName(i);
}
```

MODERN

```csharp
var results = API.StatsAndAchievements.Client.GetAchievementNames();
```

### Unity Native

Steam API makes heavy use of callbacks and callresults which is Valve's answer to deligates. In Unity we normaly use UnityEvents (for callbacks) and Actions (for callresults). Heathen's API wraps every occasion of callback and callresult with the appropreate Unity native equivlent managing the memory for you.

RAW STEAM API

```csharp
if (m_NumberOfCurrentPlayers_t == null)
    m_NumberOfCurrentPlayers_t = CallResult<NumberOfCurrentPlayers_t>.Create();
    
var handle = SteamUserStats.GetNumberOfCurrentPlayers();
m_NumberOfCurrentPlayers_t.Set(handle, (result, IOFailure) =>
{
    //Do work here
});
```

MODERN

```csharp
API.StatsAndAchievements.GetNumberOfCurrentPlayers((result, IOFailure) =>
{
    //Do work here
});
```

