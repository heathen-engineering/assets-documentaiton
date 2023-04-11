# Force Effect

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

A force effect is a configurable set of rules that describe the way in which a force will be applied. Force Effects do not describe the strength of a force or the source of the force only the maths used to apply the force to a body.

Force Effects can be used to create tractor beams, repulsed bombs, gravity wells and more and Force Effects can be configured to apply to specific or ignore specific subjects. The Force Effect its self is defined as a Scriptable Object in your Asset folder; you can create a new Force Effect configuration via

Create > Physics > Effects

This will create a new Scriptable Object which exposes any of the relevant configuration values for that effect.

![An example of a wind effect](<../../../../.gitbook/assets/image (158) (1).png>)

Each effect has unique uses and configuration and is applied in a unique way ... the following articles describe the effects included with the kit.

### Related Topics

{% embed url="https://kb.heathenengineering.com/assets/physkit/components/force-effect-source" %}

{% embed url="https://kb.heathenengineering.com/assets/physkit/components/force-effect-reciever" %}

## Custom Effects

The Force Effect system was designed to be high customizable. You can create your own unique types of Force Effects by creating a script that that derives from the ForceEffect class.

```csharp
[CreateAssetMenu(menuName = "Physics/Effects/Custom")]
public class CustomEffect : ForceEffect
{
    public override void AngularEffect(Vector3 origin, float strength, PhysicsData subject)
    {
        //Do work
    }
    
    public override void LinearEffect(Vector3 origin, float strength, PhysicsData subject)
    {
        //Do work
    }
}
```

### Angular Effect

This is only invoked for subjects that are listening for angular effects and is meant to modify the torque of the subject.

#### Origin

This is the origin of the effect as a point in world space. For [Force Effect Fields](../../components/force-effect-source/force-effect-field.md) this would be the point in space where the field originates, for Fore Effect Directions this will always be a point in space 1 unit vector away from the subject in the direction the force is applied.

#### Strength

This is the strength of the effect
