---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Input Action Name

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Input action name simplifies display of a simple single input string for a given action. This tool sets the first string name mapped to this action to the attached label.

This object has a TMPro and UGUI variant.

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class TMProInputActionName : MonoBehaviour
```

or

```csharp
public class UGUIInputActionName : MonoBehaviour
```

## Fields and Attributes

<table><thead><tr><th width="217.91333012691814">Type</th><th>Name</th><th width="316.8664058133036">Comments</th></tr></thead><tbody><tr><td><a href="../scriptable-objects/input-action-set.md">InputActionSet</a></td><td>set</td><td><p>The set the action is a member of.</p><p>Set this value or Layer value but not both.</p></td></tr><tr><td><a href="../scriptable-objects/input-action-set-layer.md">InputActionSetLayer</a></td><td>layer</td><td><p>The layer the action is a member of.</p><p>Set this value or Set value but not both.</p></td></tr><tr><td><a href="../scriptable-objects/input-action.md">InputAction</a></td><td>action</td><td>The action to fetch the glyph for</td></tr></tbody></table>

## Methods

### Refresh Name

```csharp
public void RefreshName();
```

Refreshes the name mapped to this action. This is automatically called on Start and OnEnable but can be manually refreshed as needed.
