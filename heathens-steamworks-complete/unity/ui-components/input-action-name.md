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

## Introduction

Displays the controller button reported for this specific action

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
[RequireComponent(typeof(TMPro.TextMeshProUGUI))]
public class InputActionName : MonoBehaviour
```

## Fields and Attributes

### Set

```csharp
public InputActionSet set;
```

The [Steam Input Action Set](../scriptable-objects/input-action-set.md) the action is a member of

### Layer

```csharp
public InputActionSetLayer layer;
```

The [Steam Input Action Set Layer](../scriptable-objects/input-action-set-layer.md) the action is a member of

### Action

```csharp
public InputAction action;
```

The [Steam Input Action](../scriptable-objects/input-action.md) to be displayed

## Methods

### Refresh Image

```csharp
public void RefreshName()
```

Refresh the displayed name
