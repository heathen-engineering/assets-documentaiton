# Force Effect Framework

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

PhysKit's Force Effect framework is a simple structure that allows the designer to tailor physical environments in editor for quick iteration.

{% embed url="https://www.youtube.com/watch?v=MS-f7LQX5Rw" %}

You can use Force Effects to create global or localized forces the system is composed of three basic parts

### Force Effects

These discribe how a force is applied to a body and go beyond Unity's "mode" concept.&#x20;

For example a "wind force" would likely have a degree of turbulance adjusting its direction and would apply its force based on quadratic drag ... that is an object with more drag would expirence more wind force than an object with less drag.&#x20;

Gravity in contrast to wind applies a constant acceleration force toward its point of origin, so with a singel point of origin we can simulate sphrical gravity while an origin direction would allow us to simulate localized gravity similare to a body on a planet which brings us nicely into Force Effect Sources.

You can easily create custom Force Effects using the ForceEffect base class, see the [Force Effects](../../api/force-effects.md) article for more information.

### Force Effect Source

{% hint style="info" %}
TIP

Force Effect Sources can apply multiple Force Effects, mix and match
{% endhint %}

A Force Effect Source discribes the origin and strength of a force and allows us to declare this force global or not and to limit the effects to linear and or angular.&#x20;

Global Force Effect Sources are managed by the static ForceEffects API and are read by all valid recievers.&#x20;

Local (non-global) sources only effect recievers that have triggered them.&#x20;

How you decide what sources are triggered is up to you though we have built in a system using Unity's Collider Is Trigger features.&#x20;

Recievers will test On Trigger Enter and On Trigger Exit to determin if they have entered or exited the trigger collider of a source and will activate that source on themselves is so and if not ignored.

We have two types of built in sources, and you can easily create custom sources ... see the [Force Effect Source](../../components/force-effect-source/) article for more information

### Force Effect Receiver

A Force Effect Reciever is simply the interface point for the system to operate on a body. When added to a Rigidbody it will automatically add a [Physics Data](../../components/physics-data.md) componenet providing enhanced physical information about the subject.

The [recieiver componenet](../../components/force-effect-reciever.md) can be used to adjust what sources can effect this body and in what way as well as the sinsativity of this body to forces.

## Use Cases

### Sphrical Gravity

Many a space game and cute god games depend on sphrical gravity calculations. Unity's built in gravity makess the assumption that its always directional. By using a Force Effect Field and the [Gravity Effect](../../objects/force-effect/gravity-effect.md) you can you can not only apply sphrical gravity but have its strength tapper off the further you get from the source of gravity.

You can see an example of this in the [2 Spherical Gravity](../sample-scenes/2-spherical-gravity.md) sample scene

### Localized Gravity

Creating a physics based platformer? want gravity platforms, or maybe you want different subjects to exierence different gravity and different times. Use a Force Effect Direction (or many) and apply the [Gravity Effect](../../objects/force-effect/gravity-effect.md). You can now use the ignore list on recievers to control what effect which bodies experience or you can make these non-global and use simple triggers to know what gravity a body experinces even multiple sources of gravity at once.

### Damping and Boosting

Love those racing games and shooters where some platform on the ground massivly accelerts you or slogs you down like your moving through soup. Use a Force Effect Field or Direction with the [Suspend ](../../objects/force-effect/suspend-effect.md)effect to scale down or up the subjects velocity.

### Tractor Beam

Add a [Suspend ](../../objects/force-effect/suspend-effect.md)and [Tractor ](../../objects/force-effect/tractor-effect.md)effect to a source to create a tractor beam like effect aresting the bodies current movement and bringing it closer to the source.
