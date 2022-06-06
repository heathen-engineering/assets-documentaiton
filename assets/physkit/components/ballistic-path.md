# Ballistic Path

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

![](<../../../.gitbook/assets/image (155) (1).png>)

An add on for Unity's Line Renderer this component can simulate the ballistic trajectory defined by its launch settings and optionally calculate collision and bounces.

This component on its own is useful for common cases such as showing the path of a grenade, arrow, thrown object like a basketball, etc.

This component is also an excellent demonstration of the [API.Ballistic.Raycast](../api/ballistics.md#raycast) feature.

## Fields and Attributes

### Start

The point the projectile will start at.

### Gravity

The effect of gravity

### Velocity

The velocity of the projectile

### Run on Start

Should the simulation be ran on the OnStart event from Unity

### Continuous Run

Should the simulation be updated ever frame

### Collision Layers

If we use collision what should we collide with ... set this to none to disable collision

### Resolution

How far should each step test

### Max Length

How far should the simulation test

### Max Bounces

How many bounces should be calculated, 0 to disable bounce calculation

### Bounce Damping

How much velocity should be reduced per bounce ... this is a crude simulation of Unity's "bounciness" it will not map 1 to 1 in most cases but is a fair approximation.

### Trajectory

A list of points along the path, the distance between each point is equal to the resolution

### Impacts

A list of RaycastHit values for each impact point if any

## Methods

### Simulate

Call this method to update the simulation, if you have set this Continuous Run this will be called automatically on LateUpdate.
