---
description: >-
  Physics based animation of any Transform tree. Use it on skinned meshes for
  hair, tails and similar or on normal transforms as a complex chain of physical
  joints.
---

# Verlet Integration

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/concepts/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="./">.</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Verlet is available as a stand alone asset on the Unity Asset Store and as a component of PhyKit Complete

{% embed url="https://www.youtube.com/watch?v=cxN90-kkEZ8" %}

{% embed url="https://assetstore.unity.com/packages/tools/physics/physkit-anibone-173686" %}

Verlet is a component of PhysKit that allows you to quickly and easily apply physics based dynamic animations to armature bones and general transforms. A single script added to a character can control multiple hierarchies, and the easy to use settings system lets you define common configuration settings as scriptable objects for easy referencing.\


PhysKit Verlet is included in PhysKit Complete. Save on all of Heathen Engineering's Physics tools with [PhysKit Complete](http://u3d.as/1eLA)!

## Concepts

"Verlet integration" is a commonly used approach to integrate Newtonian equations of motion into a given system. Heathen's PhysKit uses the concept to drive the change in position of transforms in a chain or hierarchy accounting for velocity change, spring forces, collision and backpropigation along the chain based on stiffness.

The Verlet Spring component can be used to simulate ropes, hair, springy props like bushes, softbody skinned meshes and much more.&#x20;

## Usage

Anything that can be expressed through the concepts of elasticity and stiffness can be driven through a Verlet Spring hierarchy.

### Physic Bone (Skinned Mesh)

Also called a dynamic bone the idea is that a skinned mesh can have extra bones not driven by classic animation clips that can be moved through physical interactions to simulate softbody physics at a fraction of the cost of per vertex mesh deformations.&#x20;

This is a common solution for long flowing hair, dangling tokens on weapons, flexible weapons like whips and flails and soft bits on characters such as long ears, zombie jiblets, big bellies, breast, etc.

![A Verlet Spring Hierarchy assigned to the bones in a pony tail hair mesh](<../../.gitbook/assets/image (161) (1) (1).png>)

### Joints and Chains

We often want to add a bit of life to our props and environments. Verlet Spring can be used to drive any hierarchy of transforms working much like a chain of spring joints only with the ability to propagate changes along its length.

![A Verlet Spring Hierarchy simulating a chain whipping around in a circle (1 Verlet Spring Sample scene)](<../../.gitbook/assets/image (170) (1) (1).png>)

![Rolling a ball through a field of a few hundred Verlet Springs](<../../.gitbook/assets/image (181) (1) (1).png>)
