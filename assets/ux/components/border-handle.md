---
description: Get a handle on window size
---

# Border Handle

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="info" %}
Part of the [Window System](../learning/core-concepts/window-tools.md) of the UX Complete asset
{% endhint %}

Meant to be added to a Unity uGUI object or similar element on a Window. This expects to be the child of a window and can be at any depth you like. Its rect is what will respond to pointer input annd manage the resize operations of the parent window.

When the user grabs and drags this componenet's RectTransform a drag delta will be calculated based on the type of handle this is. The resulting delta (difference) will be reported to the parent window and used to change the size of the window.

This does work with both the old and new Input Systems from Unity.

## Definition

### Fields and Attributes

<table><thead><tr><th width="184.37677897593124">Type</th><th width="194.9100036101649">Name</th><th width="333.5407480296978">Notes</th></tr></thead><tbody><tr><td><a href="../enums/grab-handle.md">GrabHandle</a></td><td>handle</td><td>what part of the handle is this</td></tr></tbody></table>
