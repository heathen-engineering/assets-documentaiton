# Trick Shot

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

## Introduction

<figure><img src="../../../.gitbook/assets/image (2) (6).png" alt=""><figcaption></figcaption></figure>

A simple tool able to predict the flight of a projectile including bounces and to "fire" that projectile for you. Simply attach this to your "emitter" e.g. the point of origin for your projectile and this tool does the rest.

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
public List<BallisticPath> prediction;
```

For 2D

```csharp
public List<BallisticPath2D> prediction;
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
