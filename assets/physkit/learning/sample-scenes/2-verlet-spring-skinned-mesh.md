# 2 Verlet Spring Skinned Mesh

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="1-ballistic-basics.md">Ballistics</a></td><td><a href="1-buoyancy-example.md">Buoyancy</a></td><td><a href="1-force-effect-fields.md">Force Effects</a></td><td><a href="2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../../.gitbook/assets/Verlet SkinnedMesh.png>)

This scene demonstrates the use of Verlet Spring with a skinned mesh object. In this case we have 1 Verlet Spring managing "bones" in 2 different skinned meshes (body and hair). The hair is in addition simulating collision with colliders attached to key parts of the body.

Each hierarchy in the Verlet Spring has its own configuration set by reference to [Verlet Hierarchy Settings](../../objects/verlet-hierarchy-settings.md) objects.

## What do I Learn?

1. Using [Verlet Spring](../../components/verlet-spring.md) as a "Dynamic Bone" aka "Physics Bone" (skinned mesh)
2. Setting up Verlet Spring components with [referenced configuraiton](../../objects/verlet-hierarchy-settings.md)&#x20;
3. Verlet Spring collision simulation

## Objects

### Heathens\_Test\_Female\_A

This object implements the Verlet Spring which has configured 5 hierarchies representing the left and right breast, hair and left and right glute.

Colliders have been attached to key points within the bodies transforms to allow the hair to collide with it. Each hierarchy has a configuration referenced to it according to its use and all are simulated in a single update insuring accurate interaction.
