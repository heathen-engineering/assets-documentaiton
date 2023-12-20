---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Clan List

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Displays a list of the clans the user sees e.g. is a member of or otherwise has a relationship with.

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class ClanList : MonoBehaviour
```

## Fields and Attributes

### Filter

Can only be set in the editor, Scopes the list to specific clans

```csharp
[SerializeField]
private Filter filter = Filter.Any;
```

Valid options include

* Any
* Official Groups
* Public Groups
* Non-official Groups
* Private Groups
* Followed

### Content

Can only be set in the editor, The root where new records will be spawned when found

```csharp
[SerializeField]
private Transform content;
```

### Record Template

Can only be set in the editor, The template to be cloned for each entry found

```csharp
[SerializeField]
private GameObject recordTemplate;
```

### Active Filter

Updates the filter value

```csharp
public Filter ActiveFilter { get; set; }
```

## Methods

### Clear

Clears the list of records being managed

```csharp
public void Clear()
```

### Update Display

Updates the displayed list of records

```csharp
public void UpdateDisplay()
```

### Match Filter

Returns true if the Clan priovided matches the filter value

```csharp
public bool MatchFilter(ClanData clan)
```
