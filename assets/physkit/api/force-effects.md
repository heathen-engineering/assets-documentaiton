# Force Effects

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public static class ForceEffects
```

Found in namespace:

```csharp
using HeathenEngineering.PhysKit.API;
```

### What can it do?

Used primarily by Force Effect Fields and Receivers this API manages global effects and is not intended for use by the developer.

## Global

You can access the active set of global effect sources via

```csharp
API.ForceEffects.Global;
```

This is a List of ForceEffectSources that are currently active, ForceEffectSources add and remove them selves from this when enabled / disabled.
