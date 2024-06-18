# Trick Shot Line

{% hint style="success" %}
#### Like what you are seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

This component works with and requires Trick Shot, like Trick Shot it comes in both 3D and 2D variants. The component will simply manage a Line Rinderer in order to draw a line along the path predicted by Trick Shot.

### Namespace

```csharp
namespace HeathenEngineering.UnityPhysics;
```

### Definition

Available for 3D Physics

```csharp
public class TrickShotLine : MonoBehaviour
```

And for 2D Physics

```csharp
public class TrickShotLine2D : MonoBehaviour
```

## Fields and Attributes

### Run On Start

```csharp
public bool runOnStart;
```

If true the line will be updated when the Start method is called by Unity.

### Continuous Run

```csharp
public bool continuousRun;
```

If true the component will update the line every frame calling the [Trick Shot Perdict](trick-shot.md#predict) method each frame.

