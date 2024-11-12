# Trick Shot

{% hint style="success" %}
#### Like what you are seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

## Introduction

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

This tool's primary purpose is to plan the flight of a projectile including bounces given the settings you define on it and ensure the projectile follows that path in a physically accurate way.

The tool is most useful when you need to ensure that the projectile will hit and bounce in a particular way such as in puzzle games or similar.

This tool DOES NOT handle the aiming of the projectile, it simply calculates the path that will be followed given the projectile settings and manages the projectile along that path. Aiming can be done through the [Ballistics API](../api/ballistics.md) or the [BallsiticsAim](ballistic-aim.md) tool.

### Namespace

```csharp
namespace HeathenEngineering.UnityPhysics;
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

### constant acceleration

#### For 3D

```csharp
public Vector3 constantAcceleration;
```

#### For 2D

```csharp
public Vector2 constantAcceleation;
```

this is the global constant acceleration applied to the projectile over the life of its flight. At minimal this would be at least gravity (0, -9.81, 0) by default.

{% hint style="info" %}
You can use the Constant Acceleration component to calculate a dynamic constant force at run time. This is useful if you want to use local effects such as the Magnus effect which is the effect produced by the local spin of the projectile in flight and is generally calculated as local to the emitter.

Global effects can be applied directly to the field on TrickShot by summing up the values.
{% endhint %}

### radius

```csharp
public float radius;
```

The radius of the projectile body to be used

### template

For 3D

```csharp
public BallisticPathFollow template;
```

For 2D

```csharp
public BallisticPathFollow2D template;
```

The projectile template is to be spawned when the Shot method is called.

### resolution

```csharp
public float resolution;
```

The distance between each step to be calculated there is no reason for this to be any smaller than speed multiplied by the average frame time and is generally best served as `speed * fixed delta`

### distance

```csharp
public float distance;
```

The max distance the trajectory will be calculated for. This is arc distance, not linear distance.

### collision layers

```csharp
public LayerMask collisionLayers;
```

What layers should be tested for collisions

### bounce

```csharp
public int bounces;
```

How many times should the projectile be permitted to bounce before the calculation is ended?

### bounce damping

```csharp
public float bounceDamping;
```

This is how much energy will be lost for each bounce and is similar to Unity's "bounciness" values in the Physical Material and Physical Material 2D. For example, if you set a "bounciness" of .8 then you would use a "bounceDamping" of .2 meaning 20% of the energy is lost on each impact.

### distanceIsTotalLength

```csharp
public bool distanceIsTotalLength;
```

Should the distance be measured as arc length from the start or should it be considered for each bounce independently?

### prediction

For 3D

```csharp
public List<BallisticPath> prediction;
```

For 2D

```csharp
public List<BallisticPath2D> prediction;
```

This is the resulting path predicted by the tool. each entry in the list represents 1 "segment" aka "path" where a segment is "bounce to bounce" Thus if you have 2 entries then there was at least 1 bounce.

## Methods

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
