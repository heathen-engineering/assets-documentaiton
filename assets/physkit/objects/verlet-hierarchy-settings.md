# Verlet Hierarchy Settings

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Used by the [Verlet Spring](../components/verlet-spring.md) component and related objects to define a Verlet hierarchy settings.

You can apply settings to a Verlet Hierarchy either as a constant you type into the editor

![example of settings applied as a "constant"](<../../../.gitbook/assets/image (160).png>)

Or you can create settings as Scriptable Objects so you can easily reference those settings on multiple systems

![example of settings applied as a referenced settings object](<../../../.gitbook/assets/image (171) (1) (1) (1) (1).png>)

You can create a settings object as a scriptable object by right clicking in your project and selecting

`Create > Variables > Verlet Hierarchy Settings`

This will create a new settings object that you can use to configure a named configuration set for and then reference in hierarchies as needed.

![](<../../../.gitbook/assets/image (172) (1) (1).png>)

## Fields and Attributes

<table><thead><tr><th width="176.1867087633845">Type</th><th width="196.2639619713671">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>float</td><td>updateRate</td><td>The used to scale the input time per hierarchy. This can be useful to "tighten" simulation giving crisper sharper results when set greater than 1.<br>When set less than 1 it can be used to soften results. Note this can have a strong impact on results where collision is involved.</td></tr><tr><td>Vector3</td><td>constantVelocity</td><td>A constant global velocity that is applied every step. This is most often used to simulate a gravity effect though typically should be weaker than gravities acceleration.</td></tr><tr><td>bool</td><td>clearRestingVelocity</td><td>If true then the effect of constantVelocity with the system at rest will be removed e.g. gravity will not pull a resting node down. Rest  defined as true when the node is in its initial position relative to its parnet. This is a complex concept used in a few edge cases with rotating systems.</td></tr><tr><td>float</td><td>damping</td><td>reduces the effect of forces on nodes by some ratio. This can be useful to simulate drag or resistance in a system.</td></tr><tr><td>Animation Curve</td><td>dampingCurve</td><td>scales the effect of damping across nodes based on distance from root.  </td></tr><tr><td>float</td><td>elasticity</td><td>applies a force to the node inverse to its displacement. This causes a node to return to its resting position with a force equal to the distance it is off from its resting position scaled by this value.</td></tr><tr><td>Animation Curve</td><td>elasticityCurve</td><td>scales the effect of elasticity across nodes based on distance from root.</td></tr><tr><td>float</td><td>stiffness</td><td>applies two effects.<br>1) resists change to position based on velocity.<br>2) applies the resisted velocity to the parent node in reverse order.<br><br>this can cause pressure at the end of a system to shift nodes earlier in the system.</td></tr><tr><td>Animation Curve</td><td>stiffnessCurve</td><td>scales the effect of stiffness across nodes based on distance from root.</td></tr><tr><td>float</td><td>inert</td><td>scales the adoption of root velocity change causing a node to ignore some change in position relative to its parent ... eg.. to simulate inertia (as a localized resistance to change in velocity).<br><br>If set to 1 node movement will be limited to collision and external effects. Typically this is set to 0 or some to some value less than 1 to reduce the total effect of the system.</td></tr><tr><td>Animation Curve</td><td>inertCurve</td><td>scales the effect of inert across nodes based on distance from root</td></tr><tr><td>LayerMask</td><td>collisionLayers</td><td>if collision is being tested this will be used to limit those tests to specific layers</td></tr><tr><td>float</td><td>collisionRadius</td><td>The distance from the parent axis to test for collision along. You can imagine this as a capsule collider where the node and its parent represent the tips and this radius its radius.</td></tr><tr><td>Animation Curve</td><td>radiusCurve</td><td>scales the radius for collision across nodes based on distance from root</td></tr><tr><td>float</td><td>falloffAngle</td><td>If greater than 0 this represents the max angle of displacement a node can experience due to simulation.<br><br>e.g. a value of 45 would scale the effect of simulation down to 0 at 45 degrees off from resting position.<br><br>This is used to limit the displacement of a system in a soft manner that is the strength of simulation is reduced the closer the displacement angle gets to this value.</td></tr><tr><td>Animation Curve</td><td>falloffCurve</td><td>scales the falloff angle across nodes based on distance from root</td></tr></tbody></table>

