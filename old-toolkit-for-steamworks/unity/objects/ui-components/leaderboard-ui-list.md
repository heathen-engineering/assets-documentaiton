---
description: Displaying leaderboard results with zero code
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Leaderboard UI List

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Leaderboard UI List is a simple tool that can be used to display [LeaderboardEntry ](../classes/leaderboard-entry.md)records. The Leaderboard UI List can be used in conjunction with the [Leaderboard Manager](../components/leaderboard-manager.md) to display Leaderboards in your UI with a zero code setup as is demonstrated in the [Leaderboard Sample Scene](broken-reference).

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

This is the "template" that will instantiated for each record the list displays. This template should implement a component that inherits from [ILeaderboardEntryDisplay](../programming-tools/ileaderboardentrydisplay.md). You can either create your own UI Control script and implement the [ILeaderboardEntryDisplay](../programming-tools/ileaderboardentrydisplay.md) interface or you can use the [Leaderboard Entry UI Record](leaderboard-entry-ui-record.md) we provide which has a basic implementation already done.

## Methods

### Display

```csharp
public void Display(LeaderboardEntry[] entries)
```

Calling this method will cause the Leaderboard UI List to clear any currently displayed records and to instantiate the "Template" for each entry passed in. It will attempt to get the [ILeaderboardEntryDisplay ](../programming-tools/ileaderboardentrydisplay.md)component on the Template and set it's [Entry](../programming-tools/ileaderboardentrydisplay.md#entry) field.

You can connect this method to the [Leaderboard Manager's Query Completed](../components/leaderboard-manager.md#evtquerycompleted) event to automatically display the results of any query ran on the manager. Doing this will give you a "code free" solution for displaying leaderboard entries.
