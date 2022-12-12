# Input Action Name

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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

| Type                                                                   | Name   | Comments                                                                                    |
| ---------------------------------------------------------------------- | ------ | ------------------------------------------------------------------------------------------- |
| [InputActionSet](../scriptable-objects/input-action-set.md)            | set    | <p>The set the action is a member of.</p><p>Set this value or Layer value but not both.</p> |
| [InputActionSetLayer](../scriptable-objects/input-action-set-layer.md) | layer  | <p>The layer the action is a member of.</p><p>Set this value or Set value but not both.</p> |
| [InputAction](../scriptable-objects/input-action.md)                   | action | The action to fetch the glyph for                                                           |

## Methods

### Refresh Name

```csharp
public void RefreshName();
```

Refreshes the name mapped to this action. This is automatically called on Start and OnEnable but can be manually refreshed as needed.
