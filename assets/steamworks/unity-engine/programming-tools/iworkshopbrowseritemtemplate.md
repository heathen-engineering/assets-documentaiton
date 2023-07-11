# IWorkshopBrowserItemTemplate

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

A simple interface that standardizes the concept of a chat message making it easier to create UI elements for the presentation and collection of chat messages originating from Steam Lobby, Clan and Friends.

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

This should be used to apply a specific [Workshop Item](../../objects/workshop-item.md) to this entry
