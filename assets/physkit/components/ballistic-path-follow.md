# Ballistic Path Follow

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks_Cover.jpg">Steamworks_Cover.jpg</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Used with the Trick Shot component and available in both 2D and 3D Physics versions this allows a projectile to reliably follow a pre-planned ballistics path and still remain physically simulated in that it can optionally trigger OnEnterCollision for planned bounces, it can react to unexpected collisions and it can validate bounces as well as resume dynamic physics calculations at the end of the path.

## Events

### endOfPath

For 3D

```csharp
public UnityVector3Event endOfPath;
```

For 2D

```csharp
public UnityVector2Event endOfPath;
```

This is invoked when the path ends no matter how it ends. The handler would look like

For 3D

```csharp
void Handler(float2 velocity)
{
    //The path ended with a final velocity as reported
}
```

For 2D

```csharp
void Handler(float2 velocity)
{
    //The path ended with a final velocity as reported
}
```

## Fields and Attributes

### projectile

For 3D

```csharp
public BallisticsData projectile;
```

For 2D

```csharp
public BallisticsData2D projectile;
```

Defines the nature of the projectile

### path

For 3D

```csharp
public List<BallisticPath> path;
```

For 2D

```csharp
public List<BallisticPath2D> path;
```

The assigned path for this projectile

### resumeDynamicOnEnd

```csharp
public bool resumeDynamicOnEnd;
```

If true then when the path ends for any reason the connected Rigidbody will be set to non-kinematic aka dynamic and primed with the final velocity.

### validateBounce

```csharp
public bool validateBounce;
```

If true each impact will be retested to insure the same collider is present, no changes will be made to the trajectory unless a different collider or no collider is found in which case the traverse will be ended.

### invokeOnCollisionEnter

For 3D

```csharp
public bool invokeOnCollisionEnter;
```

For 2D

```csharp
public bool invokeOnCollisionEnter2D;
```

If true then the system will simulate the OnCollisionEnter (or OnCollisionEnter2D where needed) Unity message for each impact as they occur.

### simulateCollision2D

Only applicable for 2D paths

```csharp
public bool simulateCollision2D;
```

If true this will attempt to emulate the Collision2D data passed into the OnCollisionEnter method. Note that Unity works very hard to make this as difficult as possible and does not intend for anyone to do this. We recommend you do not simulate Collision2D where OnCollisionEnter should be sufficient.

### collisionMask

```csharp
public LayerMask collisionMask;
```

What layers should validation and or dynamic collision be tested on.

### endOnCollision

```csharp
public bool endOnCollision;
```

Should the system check for unplanned collisions while traversing the path
