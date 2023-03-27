# Trick Shot

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks_Cover.jpg">Steamworks_Cover.jpg</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

### Namespace

```csharp
namespace HeathenEngineering.PhysKit;
```

### Definition

Available for 3D Physics

```csharp
public class TrickShot : MonoBehaviour
```

And for 2D Physics

```csharp
public class TrickShot2D : MonoBehaviour
```

## Fields and Attributes

### speed

```csharp
public float speed;
```

The speed of the projectile to be used

### radius

```csharp
public float radius;
```

The radius of the projectiles body to be used

### template

For 3D

```csharp
public BallisticPathFollow template;
```

For 2D

```csharp
public BallisticPathFollow2D template;
```

The projectile template to be spawned when the Shot method is called.

### resolution

```csharp
public float resolution;
```

The distance between each step to be calculated there is no reason for this to be any smaller than speed multiplied by the average frame time and is generally best served as `speed * fixed delta`

### distance

```csharp
public float distance;
```

The max distance the trajectory will be calculated for. This is arc distance not linear distance.

### collisionLayers

```csharp
public LayerMask collisionLayers;
```

What layers should be tested for collisions

### bounce

```csharp
public int bounces;
```

How many times should the projectile be permitted to bounce before the calculation is ended.

### bounceDamping

```csharp
public float bounceDamping;
```

This is how much energy will be lost for each bounce and is similar to Unity's "bounciness" values in the Physical Material and Physical Material 2D. For example if you set a "bounciness" of .8 then you would use a "bounceDamping" of .2 meaning 20% of the energy is lost on each impact.

### distanceIsTotalLength

```csharp
public bool distanceIsTotalLength;
```

Should the distance be measured as arc length from the start or should it be considered for each bounce independently.

### perdiction

For 3D

```csharp
public List<BallisticPath> perdiction;
```

For 2D

```csharp
public List<BallisticPath2D> perdiction;
```

This is the resulting path predicted by the tool. each entry in the list represents 1 "segment" aka "path" where a segment is "bounce to bounce" thus if you have 2 entries then there was at least 1 bounce.

## Methods

### Aim

```csharp
public bool Aim(Vector2 target)
```

Aims the transform at the target using the low angle considering the gravity defined for the Physics system, the speed of the projectile and desired input target. This does not assure the target will be hit in that the target may be out of range or some object in the path.

### AimHigh

```csharp
public bool AimHigh(Vector2 target)
```

Aims the transform at the target using the high angle considering the gravity defined for the Physics system, the speed of the projectile and desired input target. This does not assure the target will be hit in that the target may be out of range or some object in the path.

### Predict

```csharp
public void Predict()
```

Updates the prediction based on the current settings.

### Shoot

```csharp
public void Shoot()
```

Instantiates the template and sets it on the current predicted path.
