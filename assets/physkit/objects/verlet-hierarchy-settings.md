# Verlet Hierarchy Settings

{% hint style="success" %}
Available in PhysKit Verlet and [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

Used by the [Verlet Spring](../components/verlet-spring.md) componenet and related objects to define a Verlet hierarchy settings.

You can apply settings to a Verlet Hierarchy either as a constant you type into the editor

![example of settings applied as a "constant"](<../../../.gitbook/assets/image (157).png>)

Or you can create settings as Scriptable Objects so you can easily reference those settings on mutliple systems

![example of settings applied as a referenced settings object](<../../../.gitbook/assets/image (171).png>)

You can create a settings object as a scriptable object by right clicking in your project and selecting

`Create > Variables > Verlet Hierarchy Settings`

This will create a new settings object that you can use to configure a named configuration set for and then reference in hierarchies as needed.

![](<../../../.gitbook/assets/image (172).png>)

## Fields and Attributes

| Type            | Name                 | Comment                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| float           | updateRate           | <p>The used to scale the input time per hierarchy. This can be useful to "tighten" simulation giving crisper sharper results when set greater than 1.<br>When set less than 1 it can be used to sofften results. Note this can have a strong impact on results where collision is involved.</p>                                                                                                                   |
| Vector3         | constantVelocity     | A constant global velocity that is applied every step. This is most offten used to simulate a gravity efct though typically should be weaker than gravities acceleration.                                                                                                                                                                                                                                         |
| bool            | clearRestingVelocity | If true then the effect of constantVelocity with the system at rest will be removed e.g. gravity will not pull a resting node down. Rest  defined as true when the node is in its inital position relative to its parnet. This is a complex concept used in a few edge cases with rotating systems.                                                                                                               |
| float           | damping              | reduces the effect of forces on nodes by some ratio. This can be useful to simulate drag or resistance in a system.                                                                                                                                                                                                                                                                                               |
| Animation Curve | dampingCurve         | scales the effect of damping across nodes based on distance from root.                                                                                                                                                                                                                                                                                                                                            |
| float           | elasticity           | applies a force to the node inverse to its displacement. This causes a node to return to its resting position with a force equal to the distance it is off from its resting position scaled by this value.                                                                                                                                                                                                        |
| Animation Curve | elasticityCurve      | scales the effect of elasticity across nodes based on distance from root.                                                                                                                                                                                                                                                                                                                                         |
| float           | stiffness            | <p>applies two effects.<br>1) resists change to position based on velocity.<br>2) applies the resisted velocity to the parent node in reverse order.<br><br>this can cause presure at the end of a system to shift nodes earlier in the system.</p>                                                                                                                                                               |
| Animation Curve | stiffnessCurve       | scales the effect of stiffness across nodes based on distance from root.                                                                                                                                                                                                                                                                                                                                          |
| float           | inert                | <p>scales the adoption of root velocity change causing a node to ignore some change in position relative to its parent ... eg.. to simulate inertia (as a localized resistance to change in velocity).<br><br>If set to 1 node movement will be limited to collsion and external effects. Typically this is set to 0 or some to some value less than 1 to reduce the total effect of the system.</p>              |
| Animation Curve | inertCurve           | scales the effect of inert across nodes based on distance from root                                                                                                                                                                                                                                                                                                                                               |
| LayerMask       | collisionLayers      | if collision is being tested this will be used to limit those tests to specific layers                                                                                                                                                                                                                                                                                                                            |
| float           | collisionRadius      | The distance from the parent axis to test for collision along. You can immagin this as a capsule collider where the node and its parent represent the tips and this radius its radius.                                                                                                                                                                                                                            |
| Animation Curve | radiusCurve          | scales the radius for collision across nodes based on distance from root                                                                                                                                                                                                                                                                                                                                          |
| float           | falloffAngle         | <p>If greater than 0 this represents the max angle of displacement a node can expeerience due to simualtion.<br><br>e.g. a value of 45 would scale the effect of simulation down to 0 at 45 degrees off from resting position.<br><br>This is used to limit the displacement of a system in a soft manner that is the strength of simulation is reduced the closer the displacement angle gets to this value.</p> |
| Animation Curve | falloffCurve         | scales the falloff angle across nodes based on distance from root                                                                                                                                                                                                                                                                                                                                                 |

