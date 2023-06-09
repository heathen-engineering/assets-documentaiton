# Verlet Particle

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Used by the [Verlet Hierarch](verlet-hierarchy.md) object. This represents a particle in a Verlet Integration system. Typically you would never need to access or use this object where it is only used internally by various Verlet based tools and components.

## Fields and Attributes

<table><thead><tr><th width="176.1867087633845">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>Transform</td><td>target</td><td>The Unity Transform this particle drives</td></tr><tr><td>VerletParticle</td><td>parent</td><td>The parent particle if any</td></tr><tr><td>float</td><td>damping</td><td>The applied damping effect</td></tr><tr><td>float</td><td>elasticity</td><td>The applied elasticity effect</td></tr><tr><td>float</td><td>stiffness</td><td>The applied stiffness effect</td></tr><tr><td>float</td><td>inert</td><td>The applied inert effect</td></tr><tr><td>float</td><td>falloffAngle</td><td>The applied falloff angle</td></tr><tr><td>float</td><td>collisionRadius</td><td>The applied collision radius</td></tr><tr><td>float</td><td>distance</td><td>The distance from root</td></tr><tr><td>Vector3</td><td>addedForce</td><td>The force added since last frame</td></tr><tr><td>float</td><td>weight</td><td>The relative distance from root 0 == root, 1 = end of hierarchy</td></tr><tr><td>Vector3</td><td>position</td><td>The current simulated position (world)</td></tr><tr><td>Vector3</td><td>prevPosition</td><td>The previous simulated position (world)</td></tr><tr><td>Vector3</td><td>initLocalPosition</td><td>The initial local position (local)</td></tr><tr><td>Quaternion</td><td>initLocalRotation</td><td>The initial local rotation (local)</td></tr></tbody></table>

