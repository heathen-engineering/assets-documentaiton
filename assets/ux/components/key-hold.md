# Key Hold

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

Ever play a game that asked you to push an hold a button for some period of time to activate the action?

The Key Hold event components do just that and are designed to work with Unity's "legacy Input System"

This component is available in two flavors

### KeyHoldGameEvent

For use with Heathen Game Events

### KeyHoldUnityEvent

For use with standard Unity Events

## Definition

### Fields and Attributes

| Type       | Name            | Notes                                      |
| ---------- | --------------- | ------------------------------------------ |
| KeyCode\[] | keys            | The keys to monitor, all keys must be held |
| float      | holdTime        | How long the action should be held         |
| bool       | useUnscaledTime | Should time scale be considered            |

### Events

#### Start

Occurs when the action is first started to be held

#### Cancel

Occurs when the action is released before a complete

#### Complete

Occurs when the action is fully held for its duration

#### Progressed

Updated per frame noting the total progress
