# Buoyant Body

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../.gitbook/assets/image (159) (1) (1).png>)

Used with the Surface Tool component to simulate the effect of buoyancy on a rigidbody.

### Fields and Attributes

### Buoyancy Magnitude

Effectively the gravity applied to the buoyant body, the force of buoyancy is the inverse of this value multiplied by the volume of the subject which is submerged below the surface.&#x20;

### Active Surface

A reference to the active [Surface Tool](surface-tool.md) this is used to find the surface level and density of the environment the subject is floating in.

### Calculation Mode

The [CalculationMode ](../enums/calculation-mode.md)to use when simulating the upward force.&#x20;

* Fast\
  A basic bounding volume based calculation&#x20;
* Simple\
  Same as fast but adds an additional calculation to self right the floating subject
* Complex\
  Uses the Physics Data hull and volume information to simulate buoyant force per vertex

### Submerged Ratio

The percentage of the attached [Physics Data](physics-data.md) that is submerged under the active surface tool and thus applying a buoyant force.
