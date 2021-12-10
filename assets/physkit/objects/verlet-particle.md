# Verlet Particle

{% hint style="success" %}
Available in PhysKit Verlet and [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

Used by the [Verlet Hierarch](verlet-hierarchy.md) object. This represents a particle in a Verlet Integration system. Typically you would never need to access or use this object where it is only used internally by various Verlet based tools and compoenents.

## Fields and Attributes

| Type           | Name              | Comment                                                          |
| -------------- | ----------------- | ---------------------------------------------------------------- |
| Transform      | target            | The Unity Transform this particle drives                         |
| VerletParticle | parent            | The parent particle if any                                       |
| float          | damping           | The applied damping effect                                       |
| float          | elasticity        | The applied elasticity effect                                    |
| float          | stiffness         | The applied stiffness effect                                     |
| float          | inert             | The applied inert effect                                         |
| float          | falloffAngle      | The applied falloff angle                                        |
| float          | collisionRadius   | The applied collision radius                                     |
| float          | distance          | The distance from root                                           |
| Vector3        | addedForce        | The force added since last frame                                 |
| float          | weight            | The relative disttance from root 0 == root, 1 = end of hierarchy |
| Vector3        | position          | The current simulated position (world)                           |
| Vector3        | prevPosition      | The previous simulated postion (world)                           |
| Vector3        | initLocalPosition | The inital local position (local)                                |
| Quaternion     | initLocalRotation | The inital local rotaiton (local)                                |

