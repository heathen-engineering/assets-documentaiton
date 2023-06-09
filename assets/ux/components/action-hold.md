---
description: Push and hold to do a thing 💡
---

# Action Hold

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

Ever play a game that asked you to push an hold a button for some period of time to activate the action?

The Action Hold event componenets do just that and are designed to work with Unity's "new Input System"

This componenet is available in two flavors

### ActionHoldGameEvent

For use with Heathen Game Events

### ActionHoldUnityEvent

For use with standard Unity Events

## Definition

### Fields and Attributes

<table><thead><tr><th width="184.37677897593124">Type</th><th width="203.52728947555755">Name</th><th width="333.5407480296978">Notes</th></tr></thead><tbody><tr><td>InputAction</td><td>action</td><td>The action to monitor</td></tr><tr><td>float</td><td>holdTime</td><td>How long the action should be held</td></tr><tr><td>bool</td><td>useUnscaledTime</td><td>Should time scale be considered</td></tr></tbody></table>

### Events

#### Start

Occurs when the action is first started to be held

#### Cancel

Occurs when the action is released before a complete

#### Complete

Occurs when the action is fully held for its duration

#### Progressed

Updated per frame noting the total progress
