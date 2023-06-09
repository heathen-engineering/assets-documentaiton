# Mesh Tools

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

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
