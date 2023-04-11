# Physics Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../.gitbook/assets/image (157) (1).png>)

Creates and syncs physics data for an object beyond what is found in Unity's RigidBody. In particular the PhysicsData component will inspect all child mesh objects and create a related hull. Hull geometry is then used to calculate cross section, volumetric density, total volume and more.

## Fields and Attributes

### Debug

Only used in editor, when enabled this will cause the gizmo system to drag bounding information and velocity information in the scene window.

### Hull Geometry

```csharp
public Mesh hullGeometry;
```

The hull geometry created by the Physics Data object. This is calculated from the child meshes of the object or when the Register Geometry method is called.

### Mass

```csharp
public float Mass => get;
```

The mass of the object as seen on the attached rigidbody

### Linear Drag Coefficient

```csharp
public float LinearDragCoefficient => get;
```

The linear drag as seen on the attached rigidbody. This is used to calculate quadratic drag effects.

### Angular Drag Coefficient

```csharp
public float AngularDragCoefficient => get;
```

The angular drag as seen on the attached rigidbody. This is used to calculate quadratic drag effects.

### Density

```csharp
public float Density => get;
```

The average density of the body e.g. Mass / Volume

### Volume

```csharp
public float volume;
```

The volume of the geometry that makes up the body. This is calculated when hull geometry is calculated.

### Area

```csharp
public float area;
```

The surface area of the hull geometry. This is calculated when hull geometry is calculated.

### X Cross Section

```csharp
public float xCrossSection;
```

The effective cross section as seen from the X axis. This is calculated when hull geometry is calculated.

### Y Cross Section

```csharp
public float yCrossSection;
```

The effective cross section as seen from the Y axis. This is calculated when hull geometry is calculated.

### Z Cross Section

```csharp
public float zCrossSection;
```

The effective cross section as seen from the Z axis. This is calculated when hull geometry is calculated.

### Linear Heading

```csharp
public Vector3 LinearHeading => get;
```

The direction of travel as seen from the rigidbody.

### Linear Speed

```csharp
public float LinearSpeed => get;
```

The speed of travel as seen from the rigidbody;

### Linear Velocity

```csharp
public Vector3 LinearVelocity => get;
```

The linear velocity as seen from the rigidbody; This is the same as LinearSpeed \* LinearHeading

### Angular Heading

```csharp
public Vector3 AngularHeading => get;
```

The angular heading as seen from the rigidbody;

### Angular Speed

```csharp
public float AngularSpeed => get;
```

The angular speed as seen from the rigidbody;

### Angular Velocity

```csharp
public Vector3 AngularVelocity => get;
```

The angualge velocity as seen form the rigidbody; This is the same as AngularSpeed \* AngularHeading;

### Bounds

```csharp
public Bounds Bounds => get;
```

The bounds of the hull geometry.

### Attached Rigidbody

```csharp
public Rigidbody AttachedRigidbody => get;
```

The attached rigidbody

## Methods

### Register Geometry

```csharp
public void RegisterGeometry(IEnumerable<MeshFilter> source);
```

Calculates a hull based on 1 or more MeshFilters and uses the resulting hull to calculate volume, surface area and other related features of the system.

Note that this does not respect the ignored meshes field. you are expected to hand this method only what should be calculated.

This method is called automatically on awake but can be called manually to force and update or for procedural bodies.

### Cross Section

```csharp
public float CrossSection(Vector3 direction);
```

Estimates the effective cross section as viewed from this direction.

### Get Bound Corners

```csharp
public Vector3[] GetBoundCorners();
```

Gets the corners of the bounding box around the body based on the hull mesh

