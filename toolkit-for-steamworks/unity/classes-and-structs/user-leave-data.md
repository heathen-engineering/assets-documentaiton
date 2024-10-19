---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# User Leave Data

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public struct UserLeaveData
```

Used in the GameConnectedChatLeaveEvent and related event handlers.

## Fields and Attributes

### Room

The chat room this data relates to

```csharp
public ChatRoom room;
```

### User

The user this data relates to

```csharp
public UserData user;
```

### Kicked

Was the user kicked out

```csharp
public bool kicked;
```

### Dropped

Was the connection dropped

```csharp
public bool dropped;
```
