# Buoyancy

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public static class Buoyancy
```

Found in namespace:

```csharp
using HeathenEngineering.UnityPhysics.API;
```

{% hint style="info" %}
We recommend using aliases to reduce typing and simplify names.



```csharp
using API = HeathenEngineering.UnityPhysics.API;
```

doing this you can fully qualify the name of this class as

```csharp
API.Ballistics
```
{% endhint %}

### What can it do?

This API is used to calculate the effective buoyancy force applied to a body given that bodies physics data and information about the environment its in.

Put more simply we can use this to make things float.

## Effect

The main function of this API is to calculate the buoyancy effect. That is to tell us how much force is being applied counter to gravity. Note we don't need to know what direction that is only how strong the effect is we can then use that information along with other physics data to simulate a floating object.

Effect can be calculated in three ways

```csharp
public static float Effect(
    PhysicsData data, //The body we are testing
    SurfaceTool surface, //The environment we are testing in
    float gravity, //The magnitude/strength of gravity
    out List<PointVolume> submergedPoints, //The points under the surface
    out float volume) //The dispacement of the surface (volume submerged)
```

This is the most complex method and pulls hull information from the provided [PhysicsData](../components/physics-data.md) to test each vertex point giving a reasonably accurate estimate on the submerged volume. You can use the submergedPoints returned and the ratio of the total submerged volume to distribute the applied force across the subject. This is the method used by the [Buoyant Body](../components/buoyant-body.md) when in complex mode.

A simpler and generally more stable method for most use cases is:

```csharp
public static Effect(
    PhysicsData data, //The body we are testing
    SurfaceTool surface, //The environment we are testing in
    float gravity, //The magnitude/strength of gravity
    out float volume) //The displacement of the surfce (volume submerged)
```

The final method is the simplest but makes the most assumptions.

```csharp
public static Effect(
    float displacementVolume, //The amount of the volume displaced
    float density, //The density of the volume we are in
    float gravityMagnitude) //The strength of gravity
```

This expects you to provide it with the volume of the geometry submerged and the density of the environment the body is in.

## Displacement

Finds the volume of the provided mesh that is displacing the target surface volume.

```csharp
public static float Displacement(
    Transform root, // Root of the mesh
    Mesh mesh, // The mesh to test for
    Vector3 scale, // The relative scale of the mesh
    SurfaceTool surface) // the surface volume to test
```
