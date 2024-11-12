---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Clan Chat Member List

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Displays a list of the members that are in a specific clan chat.

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class ClanChatMemberList : MonoBehaviour
```

## Fields and Attributes

### Clan Id

Only assignable in the Unity Editor, this is the ID of the clan you would like to display members for

```csharp
[SerializeField]
private ulong clanId;
```

### Content

The root where the UI elements representing each user will be spawned

```csharp
[SerializeField]
private Transform content;
```

### Template

The template that will be spawned for each member found in the list, this should have a component on it that implements the [IUserProfile](../programming-tools/iuserprofile.md) interface

```csharp
[SerializeField]
private GameObject template;
```

### Clan

The [Clan Data ](../classes-and-structs/clan-data.md)object for the linked clan

```csharp
public ClanData Clan { get; set; )
```

## Methods

### Apply

Set the clan this object is tracking

```csharp
public void Apply(ClanData clan)
```

### Refresh

Refresh the display of records

```csharp
public void Refresh()
```
