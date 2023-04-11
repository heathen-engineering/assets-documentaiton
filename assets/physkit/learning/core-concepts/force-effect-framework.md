# Force Effect Framework

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

PhysKit's Force Effect framework is a simple structure that allows the designer to tailor physical environments in editor for quick iteration.

{% embed url="https://www.youtube.com/watch?v=MS-f7LQX5Rw" %}

You can use Force Effects to create global or localized forces the system is composed of three basic parts

### Force Effects

These describe how a force is applied to a body and go beyond Unity's "mode" concept.&#x20;

For example a "wind force" would likely have a degree of turbulence adjusting its direction and would apply its force based on quadratic drag ... that is an object with more drag would experience more wind force than an object with less drag.&#x20;

Gravity in contrast to wind applies a constant acceleration force toward its point of origin, so with a single point of origin we can simulate spherical gravity while an origin direction would allow us to simulate localized gravity similar to a body on a planet which brings us nicely into Force Effect Sources.

You can easily create custom Force Effects using the ForceEffect base class, see the [Force Effects](../../api/force-effects.md) article for more information.

### Force Effect Source

{% hint style="info" %}
TIP

Force Effect Sources can apply multiple Force Effects, mix and match
{% endhint %}

A Force Effect Source describes the origin and strength of a force and allows us to declare this force global or not and to limit the effects to linear and or angular.&#x20;

Global Force Effect Sources are managed by the static ForceEffects API and are read by all valid receivers.&#x20;

Local (non-global) sources only effect receivers that have triggered them.&#x20;

How you decide what sources are triggered is up to you though we have built in a system using Unity's Collider Is Trigger features.&#x20;

Receivers will test On Trigger Enter and On Trigger Exit to determine if they have entered or exited the trigger collider of a source and will activate that source on themselves is so and if not ignored.

We have two types of built in sources, and you can easily create custom sources ... see the [Force Effect Source](../../components/force-effect-source/) article for more information

### Force Effect Receiver

A Force Effect Receiver is simply the interface point for the system to operate on a body. When added to a Rigidbody it will automatically add a [Physics Data](../../components/physics-data.md) component providing enhanced physical information about the subject.

The [recieiver componenet](../../components/force-effect-reciever.md) can be used to adjust what sources can effect this body and in what way as well as the sensitivity of this body to forces.

## Use Cases

### Spherical Gravity

Many a space game and cute god games depend on spherical gravity calculations. Unity's built in gravity makes the assumption that its always directional. By using a Force Effect Field and the [Gravity Effect](../../objects/force-effect/gravity-effect.md) you can you can not only apply spherical gravity but have its strength tapper off the further you get from the source of gravity.

You can see an example of this in the [2 Spherical Gravity](../sample-scenes/2-spherical-gravity.md) sample scene

### Localized Gravity

Creating a physics based platformer? want gravity platforms, or maybe you want different subjects to experience different gravity and different times. Use a Force Effect Direction (or many) and apply the [Gravity Effect](../../objects/force-effect/gravity-effect.md). You can now use the ignore list on receivers to control what effect which bodies experience or you can make these non-global and use simple triggers to know what gravity a body experiences even multiple sources of gravity at once.

### Damping and Boosting

Love those racing games and shooters where some platform on the ground massively accelerates you or slogs you down like your moving through soup. Use a Force Effect Field or Direction with the [Suspend ](../../objects/force-effect/suspend-effect.md)effect to scale down or up the subjects velocity.

### Tractor Beam

Add a [Suspend ](../../objects/force-effect/suspend-effect.md)and [Tractor ](../../objects/force-effect/tractor-effect.md)effect to a source to create a tractor beam like effect arresting the bodies current movement and bringing it closer to the source.
