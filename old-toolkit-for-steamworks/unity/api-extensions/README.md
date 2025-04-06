---
description: The Heathen Steam API wrapper
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# API Extensions

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Heathen API provides access to the full Steam API wrapping every interface with a Unity friendly static class, simplifying use of the raw API without reducing its functionality and exposing every callback as a UnityEvent and every callresult as a Unity firendly Action.

We have wrapped every interface (except Networking interfaces) and copied its relevant documentation meaning you can now explore Valve's own documentation in your IDE via [IntelliSense](../../../company/development/intellisense.md), take full advantage of auto complete and suggestions and explore the full API via the object explorer.&#x20;

{% hint style="info" %}
Why not wrap the networking interfaces?

We feel networking is best served working directly against the API with no "middle layer" sitting between. We are happy to revisit this if there is a community demand for it.
{% endhint %}

### Is this just Facepunch from Heathen?

No

We are still built on top of Steamworks.NET something we feel strongly about as it provides an unadulterated view of the Steam API making it possible for you to leverage decades of community guides, sample code, the official Steam Developer forums and support channels from Valve, etc.

Heathen's API does wrap the raw Steam API up as an extension to Steamworks.NET making it not just C# friendly but more Unity native. You could say what Facepunch does for a C# programmer Heathen does for a Unity programmer, Unity designer, C# programmer, C/C++ programmer, etc. but we do a lot more on top of that with our components and objects built on top of this layer.

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

Valve's Steam API is big, powerful and written in C and C++ ... not exactly friendly to many of the tried and true patterns and structures we use in C#. Heathen's API still exposes the traditional methods but also provides C# based alternatives.

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

Steam API makes heavy use of callbacks and callresults which is Valve's answer to delegates. In Unity we normally use UnityEvents (for callbacks) and Actions (for callresults). Heathen's API wraps every occasion of callback and callresult with the appropriate Unity native equivalent managing the memory for you.

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

