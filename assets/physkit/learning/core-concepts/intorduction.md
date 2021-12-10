---
description: >-
  Physics based animation of any Transform tree. Use it on skinned meshes for
  hair, tails and similar or on normal transforms as a complex chain of physical
  joints.
---

# Verlet Integration

## Introduction

Verlet is available as a stand alone asset on the Unity Asset Store and as a component of PhyKit Complete

{% embed url="https://assetstore.unity.com/packages/tools/physics/physkit-anibone-173686" %}

Verlet is a component of PhysKit that allows you to quickly and easily apply physics based dynamic animations to armature bones and general transforms. A single script added to a character can control multiple hierarchies, and the easy to use settings system lets you define common configuration settings as scriptable objects for easy referencing.\


PhysKit Verlet is included in PhysKit Complete. Save on all of Heathen Engineering's Physics tools with [PhysKit Complete](http://u3d.as/1eLA)!

## Concepts

"Verlet integration" is a commonly used approch to integrate Newtonian equations of motion into a given system. Heathen's PhysKit uses the concept to drive the change in position of transforms in a chain or hierarchy accounting for velocity change, spring forces, collision and backpropigation along the chain based on stiffness.

The Verlet Spring componenet can be used to simulate ropes, hair, springy props like bushes, softbody skinned meshes and much more.&#x20;

## Usage

Anything that can be expressed through the concepts of elaciticity and stiffness can be driven through a Verlet Spring hierarchy.

### Physic Bone (Skinned Mesh)

Also called a dynamic bone the idea is that a skinned mesh can have extra bones not driven by classic animation clips that can be moved through physical interactions to simulate softbody physics at a fraction of the cost of per vertex mesh deformations.&#x20;

This is a common soluition for long flowing hair, dangling tokens on weapons, flexable weapons like whips and flails and soft bits on characters such as long ears, zombie jiblets, big bellies, breast, etc.

![A Verlet Spring Hierarchy assigned to the bones in a pony tial hair mesh](<../../../../.gitbook/assets/image (159).png>)

### Joints and Chains

We offten want to add a bit of life to our props and environments. Verlet Spring can be used to drive any hierarchy of transforms working much like a chain of spring joints only with the ability to propigate changes along its length.

![A Verlet Spring Hirarchy simulating a chain whipping around in a circle (1 Verlet Spring Sample scene)](<../../../../.gitbook/assets/image (170).png>)

![Rolling a ball through a field of a few hundred Verlet Springs](<../../../../.gitbook/assets/image (181).png>)
