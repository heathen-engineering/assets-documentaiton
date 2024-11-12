---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# IWorkshopBrowserItemTemplate

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

A simple interface that standardizes the concept of a Workshop Browser Item making it easier to create UI elements for the presentation and collection of [Workshop items](../classes-and-structs/workshop-item.md) originating from UGC Query and similar.

```csharp
using HeathenEngieering.SteamworksIntegration.UI;
```

```csharp
public interface IWorkshopBrowserItemTemplate;
```

## Methods

### Load

```csharp
void Load(WorkshopItem item)
```

This should be used to apply a specific [Workshop Item](../classes-and-structs/workshop-item.md) to this entry
