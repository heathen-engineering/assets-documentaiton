# 1 Buoyancy Example

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="1-buoyancy-example.md">Buoyancy</a></td><td><a href="1-force-effect-fields.md">Force Effects</a></td><td><a href="2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../../.gitbook/assets/image (175) (1).png>)

This scene demonstrates the use of the [Buoyancy Body](../../components/buoyant-body.md). [Buoyancy Body Drag](../../components/buoyant-body-drag.md) and [Surface Tool](../../components/surface-tool.md) components. The sample scene uses a custom [Surface Tool](../../components/surface-tool.md) to simulate a crude wave effect to demonstrate how you might connect Surface Tool to whatever water/ocean simulation tool you prefer to use.

The example [Surface Tool](../../components/surface-tool.md) (WaveSurface) defines the surface of the volume and the density of the volume.

The [Buoyancy Body](../../components/buoyant-body.md) uses the Surface Tool along with the Buoyancy API to calculate and apply a buoyant force on the attached body.

The [Buoyancy Body Drag](../../components/buoyant-body-drag.md) tool works with the Buoyancy Body to modify the applied drag on the body causing it to experience more drag the more "water" its drafting.

## What do I Learn?

1. How to access the [Buoyancy API](../../api/buoyancy.md) from your scripts
2. How to use [Buoyancy Body](../../components/buoyant-body.md)
3. How to use [Buoyancy Body Drag](../../components/buoyant-body-drag.md)
4. Hot to create and use a custom [Surface Tool](../../components/surface-tool.md)

## Objects

### Test Float

The scene has 4 Test Float objects

* Test Float (Player)
* Test Float (1)
* Test Float (2)
* Test Float (3)

The Test Float objects implement the [Buoyant Body](../../components/buoyant-body.md) and [Buoyant Body Drag](../../components/buoyant-body-drag.md) components which them selves require and apply a [Physics Data](../../components/physics-data.md) component. These 3 components allow the objects to float on the surface of the Ocean component which implements a Surface Tool.

#### Test Float (Player)&#x20;

This float object implements an addition sample script which serves as a crude player controller e.g. moves when the WASD keys are pressed.

### Cubes

The scene has 320 cube objects equipped with the same basic behaviors as the board configured to use a fast float. These simply serve to demonstrate the efficiency of the effect.

### Ocean

The Ocean object implements the custom script WaveSurface which is a sample implementation of the [Surface Tool](../../components/surface-tool.md).

#### WaveSurface.cs

This script is a crude example for a water/ocean [SurfaceTool](../../components/surface-tool.md). Typically your custom SurfaceTool would simply find the depth from surface at any given world point. This sample script does that and also simulates a simple wave effect.

To learn more about [Surface Tool](../../components/surface-tool.md) please see the [Surface Tool Article](../../components/surface-tool.md).
