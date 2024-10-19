---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Set User Id Label

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Displays the ID of a friend in a text label

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class ClanProfile : MonoBehaviour
```

## Fields and Attributes

### As Hex

Should the ID be displayed as a Hex value

```csharp
public bool AsHex { get; set; }
```

### User Data

What user is currently applied

```csharp
public UserData UserData { get; set; }
```

## Methods

### Apply

Applies a user to be displayed

```csharp
public void Apply(UserData user)
```
