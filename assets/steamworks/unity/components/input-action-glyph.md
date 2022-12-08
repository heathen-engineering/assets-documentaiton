# Input Action Glyph

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The Input action glyph simplifies display of a simple single input image for a given action. This tool sets the first glyph image mapped to this action to the attached RawImage texture.

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class InputActionGlyph : MonoBehaviour
```

## Fields and Attributes

| Type                                                                   | Name   | Comments                                                                                    |
| ---------------------------------------------------------------------- | ------ | ------------------------------------------------------------------------------------------- |
| [InputActionSet](../scriptable-objects/input-action-set.md)            | set    | <p>The set the action is a member of.</p><p>Set this value or Layer value but not both.</p> |
| [InputActionSetLayer](../scriptable-objects/input-action-set-layer.md) | layer  | <p>The layer the action is a member of.</p><p>Set this value or Set value but not both.</p> |
| [InputAction](../scriptable-objects/input-action.md)                   | action | The action to fetch the glyph for                                                           |

## Methods

### Refresh Image

```csharp
public void RefreshImage();
```

Refreshes the image mapped to this action. This is automatically called on Start and OnEnable but can be manually refreshed as needed.
