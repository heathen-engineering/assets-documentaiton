# Verlet Spring

{% hint style="success" %}
Available in PhysKit Verlet and [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

![](<../../../.gitbook/assets/image (166) (1) (1) (1).png>)

The Verlet Spring componenet manages hierarchies of transforms integrating Newtonian movement formulas according to the settings applied to each hierarchy.

In simpler terms it lets you discribe how a chain of transforms should act physicaly speaking.

Each Verlet Spring componenet can manage any number of hierarchies, each componenet updates all of the hierachies defined in it so you can use this concept to group systems together making it easier to turn them on and off.

For example you would add a Verlet Spring componenet to a character and then create hierarchies for that characters required parts. Then when that character is disabled its Verlet calculations are also disabled.

## Fields and Attributes

### Transform Hierarchies

```csharp
public List<VerletHierarchy> transformHierarchies;
```

The list of [hierarches ](../objects/verlet-hierarchy.md)managed by the spring

You can manaually add hierarchies by first constructing a higharchy and adding it to the list

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
