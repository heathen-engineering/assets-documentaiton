# Mesh Tools

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public static class MeshTools
```

Found in namespace:

```csharp
using HeathenEngineering.PhysKit.API;
```

{% hint style="info" %}
We recomend using aliases to reduce typing and simplify names. and reduce possible collisions with similarly named objects.



```csharp
using API = HeathenEngineering.PhysKit.API;
```

doing this you can fully qualify the name of this class as

```csharp
API.MeshTools
```
{% endhint %}

### What can it do?

Mesh tools is used to create convex hulls, calculate the volume of a mesh, find surface area and various other geometry functions handy when your working on physics problems.

## Convex Hull

The most common use of mesh tools is to create a convex hull. You can get a convex hull for a single mesh, multiple mesh or for any collection of points in space.

```csharp
var mesh = MeshTools.ConvexHull(meshfilters);
```

```csharp
var mesh = MeshTools.ConvexHull(meshes);
```

```csharp
var mesh = MeshTools.ConvexHull(vertexList);
```

## Mesh Volume

You can find the volume of a mesh, or find the convex hull of a mesh then find the volume of that

```csharp
var volume = MeshTools.VolumeOfConvexMesh(mesh, scale);
```

or

```csharp
var volume = MeshTools.VolumeOfMesh(mesh, scale);
```

## Surface Area

### Whole Mesh

```csharp
var surface = MeshTools.SurfaceArea(mesh);
```

### Cross Section area

```csharp
var surface = MeshTools.FacingSurfaceArea(mesh, direction);
```

## Area and Volume

A quick short cut to do both&#x20;

```csharp
MeshTools.GetAreaAndVolume(mesh, scale, out surface, out volume);
```
