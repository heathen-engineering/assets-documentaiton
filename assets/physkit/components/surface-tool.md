# Surface Tool

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

Surface Tool is meant to be inherited from to create a custom Surface based on your choosen ocean or water simulation tool. The purpose of Surface Tool is simply to find the depth and surface normal based on world point.

Most water and ocean simulation systems simulate waves across the surface that floating objects should respond to. For the Buoyancy system to work it needs to find the depth (downward distnace from surface) at any given world point and to find the surface normal of the surface at that point.

A crude example of this is demonstrated in the Sample script WaveSurface.cs. The WaveSurface uses a simple perlin noise calculation to simulate swells and uses that information to both drive a simple shader rendering the swells and to implament the SurfaceDepth and SurfaceNormal methods.

## Methods

### SurfaceDepth

```csharp
public override float SurfaceDepth(Vectror3 worldPosition);
```

Override this method which should return the signed distnace from the surface at this point.

### SurfaceNormal

```csharp
public override Vector3 SurfaceNormal(Vector3 worldPoint);
```

Override this method which should return the surface normal at the point on surface above or below this world point.&#x20;
