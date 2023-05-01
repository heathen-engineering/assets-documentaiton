---
description: Displaying leaderboard results with zero code
---

# Leaderboard UI List

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Leaderboard UI List is a simple tool that can be used to display [LeaderboardEntry ](../../objects/leaderboard-entry.md)records. The Leaderboard UI List can be used in conjunction with the [Leaderboard Manager](leaderboard-manager.md) to display Leaderboards in your UI with a zero code setup as is demonstrated in the [Leaderboard Sample Scene](../../unity-engine/sample-scenes/leaderboards.md).

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration.UI;
```

### Definition

```csharp
public class LeaderboardUIList : MonoBehaviour
```

## Events

### Enabled

```csharp
public UnityEvent Enabled;
```

This is called when the list is enabled and can be useful when you want to refresh a query when enabling (showing) the UI element.

## Fields and Attributes

### Collection

```csharp
public Transform collection;
```

This will be the parent of any records instantiated by the tool. Most often you would set this to be the `Content` GameObject of a ScrollRect or similar.

### Template

```csharp
public GameObject template;
```

This is the "template" that will instantiated for each record the list displays. This template should implement a component that inherits from [ILeaderboardEntryDisplay](../interfaces/ileaderboardentrydisplay.md). You can either create your own UI Control script and implement the [ILeaderboardEntryDisplay](../interfaces/ileaderboardentrydisplay.md) interface or you can use the [Leaderboard Entry UI Record](leaderboard-entry-ui-record.md) we provide which has a basic implementation already done.

## Methods

### Display

```csharp
public void Display(LeaderboardEntry[] entries)
```

Calling this method will cause the Leaderboard UI List to clear any currently displayed records and to instantiate the "Template" for each entry passed in. It will attempt to get the [ILeaderboardEntryDisplay ](../interfaces/ileaderboardentrydisplay.md)component on the Template and set it's [Entry](../interfaces/ileaderboardentrydisplay.md#entry) field.

You can connect this method to the [Leaderboard Manager's Query Completed](leaderboard-manager.md#evtquerycompleted) event to automatically display the results of any query ran on the manager. Doing this will give you a "code free" solution for displaying leaderboard entries.
