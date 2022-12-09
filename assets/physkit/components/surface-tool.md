# Surface Tool

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Surface Tool is meant to be inherited from to create a custom Surface based on your chosen ocean or water simulation tool. The purpose of Surface Tool is simply to find the depth and surface normal based on world point.

Most water and ocean simulation systems simulate waves across the surface that floating objects should respond to. For the Buoyancy system to work it needs to find the depth (downward distance from surface) at any given world point and to find the surface normal of the surface at that point.

A crude example of this is demonstrated in the Sample script WaveSurface.cs. The WaveSurface uses a simple perlin noise calculation to simulate swells and uses that information to both drive a simple shader rendering the swells and to implement the SurfaceDepth and SurfaceNormal methods.

## Methods

### SurfaceDepth

```csharp
public override float SurfaceDepth(Vectror3 worldPosition);
```

Override this method which should return the signed distance from the surface at this point.

### SurfaceNormal

```csharp
public override Vector3 SurfaceNormal(Vector3 worldPoint);
```

Override this method which should return the surface normal at the point on surface above or below this world point.&#x20;
