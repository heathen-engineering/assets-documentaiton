# Verlet Spring

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../.gitbook/assets/image (166) (1) (1) (1) (1) (1).png>)

The Verlet Spring component manages hierarchies of transforms integrating Newtonian movement formulas according to the settings applied to each hierarchy.

In simpler terms it lets you describe how a chain of transforms should act physically speaking.

Each Verlet Spring component can manage any number of hierarchies, each component updates all of the hierarchies defined in it so you can use this concept to group systems together making it easier to turn them on and off.

For example you would add a Verlet Spring component to a character and then create hierarchies for that characters required parts. Then when that character is disabled its Verlet calculations are also disabled.

## Fields and Attributes

### Transform Hierarchies

```csharp
public List<VerletHierarchy> transformHierarchies;
```

The list of [hierarches ](../objects/verlet-hierarchy.md)managed by the spring

You can manually add hierarchies by first constructing a hierarchy and adding it to the list

```csharp
var nTree = new VerletHierarchy
{
    root = rootTransform,
    nodes = new List<VerletParticle>(),
    ignoreList = new List<Transform>(),
    settings = new VerletHierarchySettingsReference(new VerletHierarchSettings())
};
//Add any transforms you want to exclude ... 
//all children of that tranform will also be excluded
nTree.ignoreList.Add(ignoreThisOne);
//This populates the nTree.nodes
nTree.RegisterNodes();

spring.transformHierarchies.Add(nTree);
```

## Methods

### Add Force

You can add additional forces to hierarchies to simulate effects like explosions, wind, etc. To add a force you can use

```csharp
spring.AddForce(Vector3 force);
```

This will add the force evenly to all hierarchies and nodes with in each hierarchy and is useful for global effects like gravity, wind or buoyancy

```csharp
spring.AddForceAtPosition(float forceMagnitude, Vector3 position);
```

This will apply a positional force and is more useful for effects like explosions.

{% hint style="info" %}
These methods are just shortcuts to effect all Hierarchies within the spring, you can applies these to specific hierarchies if you like. See [Verlet Hierarchy](../objects/verlet-hierarchy.md) for more information
{% endhint %}
