# 2 Spherical Gravity

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="1-ballistic-basics.md">Ballistics</a></td><td><a href="1-buoyancy-example.md">Buoyancy</a></td><td><a href="1-force-effect-fields.md">Force Effects</a></td><td><a href="2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../../.gitbook/assets/Sphere Grav.png>)

This scene demonstrates a more typical use of the [Force Effect framework](../core-concepts/force-effect-framework.md); spherical gravity. You will find a sphere center of the screen with a number of objects placed around it. The sphere has a [Force Effect Field](../../components/force-effect-source/force-effect-field.md) configured to use the [Gravity Effect](../../objects/force-effect/gravity-effect.md).&#x20;

## What do I Learn?

1. What is a [Force Effect](../../api/force-effects.md)
2. What is a [Force Effect Source](../../components/force-effect-source/)
3. What is a [Force Effect Reciever](../../components/force-effect-reciever.md)&#x20;
4. Use of the [Gravity Effect](../../objects/force-effect/gravity-effect.md)

## Objects

### Planet

The planet is a simple sphere mesh along with a [Force Effect Field](../../components/force-effect-source/force-effect-field.md) with the [Gravity Effect](../../objects/force-effect/gravity-effect.md) configured.

### Objects

This is a collection of spheres and cubes configured as [Force Effect Receivers](../../components/force-effect-reciever.md)
