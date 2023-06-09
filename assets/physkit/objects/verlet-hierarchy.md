# Verlet Hierarchy

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Used by the [Verlet Spring](../components/verlet-spring.md) component to define a Verlet hierarchy.

## Fields and Attributes

<table><thead><tr><th width="176.1867087633845">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>Transform</td><td>root</td><td>The root of the hierarchy. This node will not be moved but may rotate.</td></tr><tr><td>VerletHierarchySettingsReference</td><td>settings</td><td>Scriptab Reference for <a href="verlet-hierarchy-settings.md">VerletHierarchySettings</a>.</td></tr><tr><td>List&#x3C;<a href="verlet-particle.md">VerletParticle</a>></td><td>nodes</td><td>The list of particles managed by this system</td></tr><tr><td>List&#x3C;Transform></td><td>ignoreList</td><td>The transforms to exclude from simulation when registering particles</td></tr><tr><td>Vector3</td><td>restingVelocity</td><td>The constant velocity to remove from input velocity ... typically this is set as the local direction of acceleration of gravity when the system is at rest. <br><br>This is typically only used by internal updates when the use resting flag is enabled in the <a href="verlet-hierarchy-settings.md">VerletHierarchy settings</a>. </td></tr></tbody></table>

## Methods

### Add Force

You can add additional forces to the hierarchy in one of two ways

```csharp
public void AddForce(Vector3 force);
```

This will apply the force evenly to all nodes in the hierarchy and is useful for global forces such as wind, gravity and buoyancy.

```csharp
public void AddForceAtPosition(float forceMagnitude, Vector3 position);
```

This is usefor for positional forces such as explosions.

### Register Nodes

```csharp
public void RegisterNodes();
```

This simply walks the transform hierarchy of the root attribute and creates [VerletParticle ](verlet-particle.md)entries for any transform that is not being ignored. This is typically only ever called on create and typically at development time in the Unity Editor but can be used at run time if needed.

### ResetNodes

```csharp
public void ResetNodes();
```

This is used to put all particles back to there initial states and is called when registering nodes at run time. In general it shouldn't need to be called manually.

### Update

```csharp
public void Update(Vector3 velocity, float time);
```

This is called by the Verlet Spring to update the system and generally shouldn't be called manually.

Note velocity is applied as a global effect scaled by the inert setting value, time is the step in time to be simulated and is typically the Fixed Delta Time but may be scaled to "tighten" the simulation.
