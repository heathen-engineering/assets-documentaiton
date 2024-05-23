---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Clan Profile

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Displays the icon, name and tag of a given clan

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class ClanProfile : MonoBehaviour
```

## Fields and Attributes

### Clan

The clan to be displayed

```csharp
public ClanData Clan { get; set; }
```

## Methods

### Apply

Sets the clan to be displayed

```csharp
public void Apply(ClanData clan)
```
