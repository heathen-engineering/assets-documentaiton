---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Clan Chat Member Counter

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Maintains a display of the number of users in a clan chat.

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class ClanChatMemberCounter : MonoBehaviour
```

## Fields and Attributes

### Clan Id

Can only be set in the Unity Editor

The ID of the clan to monitor

```csharp
[SerializeField]
private ulong clanId;
```

### Prefix

Can only be set in the Unity Editor

The prefix to assign to the text label before the number of users

```csharp
[SerializeField]
internal string prefix;
```

### Suffix

Can only be set in the Unity Editor

The suffix to assign to the text label after the number of users

```csharp
[SerializeField]
internal string suffix;
```

### Clan

Exposes the [ClanData ](../classes-and-structs/clan-data.md)that this object is linked to and can be assigned to update which clan is monitored

```csharp
public ClanData Clan { get; set; }
```

## Methods

### Apply

Apply the clan, this is done for you when you assign the Clan field

```csharp
public void Apply(ClanData clan)
```

### Refresh

Refresh the value, this updates the text label, this is in general called for you

```csharp
public void Refresh()
```

