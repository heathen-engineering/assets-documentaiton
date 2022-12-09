# Verlet Hierarchy

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Used by the [Verlet Spring](../components/verlet-spring.md) component to define a Verlet hierarchy.

## Fields and Attributes

| Type                                       | Name            | Comment                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Transform                                  | root            | The root of the hierarchy. This node will not be moved but may rotate.                                                                                                                                                                                                                                                                       |
| VerletHierarchySettingsReference           | settings        | Scriptab Reference for [VerletHierarchySettings](verlet-hierarchy-settings.md).                                                                                                                                                                                                                                                              |
| List<[VerletParticle](verlet-particle.md)> | nodes           | The list of particles managed by this system                                                                                                                                                                                                                                                                                                 |
| List\<Transform>                           | ignoreList      | The transforms to exclude from simulation when registering particles                                                                                                                                                                                                                                                                         |
| Vector3                                    | restingVelocity | <p>The constant velocity to remove from input velocity ... typically this is set as the local direction of acceleration of gravity when the system is at rest. <br><br>This is typically only used by internal updates when the use resting flag is enabled in the <a href="verlet-hierarchy-settings.md">VerletHierarchy settings</a>. </p> |

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
