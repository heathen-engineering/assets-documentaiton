# Verlet Particle

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Used by the [Verlet Hierarch](verlet-hierarchy.md) object. This represents a particle in a Verlet Integration system. Typically you would never need to access or use this object where it is only used internally by various Verlet based tools and components.

## Fields and Attributes

| Type           | Name              | Comment                                                         |
| -------------- | ----------------- | --------------------------------------------------------------- |
| Transform      | target            | The Unity Transform this particle drives                        |
| VerletParticle | parent            | The parent particle if any                                      |
| float          | damping           | The applied damping effect                                      |
| float          | elasticity        | The applied elasticity effect                                   |
| float          | stiffness         | The applied stiffness effect                                    |
| float          | inert             | The applied inert effect                                        |
| float          | falloffAngle      | The applied falloff angle                                       |
| float          | collisionRadius   | The applied collision radius                                    |
| float          | distance          | The distance from root                                          |
| Vector3        | addedForce        | The force added since last frame                                |
| float          | weight            | The relative distance from root 0 == root, 1 = end of hierarchy |
| Vector3        | position          | The current simulated position (world)                          |
| Vector3        | prevPosition      | The previous simulated position (world)                         |
| Vector3        | initLocalPosition | The initial local position (local)                              |
| Quaternion     | initLocalRotation | The initial local rotation (local)                              |

