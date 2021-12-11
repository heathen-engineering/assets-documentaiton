# Force Effect



{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

A force effect is a configurable set of rules that discribe the way in which a force will be applied. Force Effects do not discribe the strength of a force or the source of the force only the maths used to apply the force to a body.

Force Effects can be used to create tractor beams, repulsor bombs, gravity wells and more and Force Effects can be configured to apply to specific or ignore specific subjects. The Force Effect its self is defined as a Scriptable Object in your Asset folder; you can create a new Force Effect configuration via

Create > Physics > Effects

This will create a new Scriptable Object which exposes any of the relivent configuration values for that effect.

![An example of a wind effect](<../../../../.gitbook/assets/image (158).png>)

Each effect has unique uses and configuration and is applied in a unique way ... the following articles discribe the effects included with the kit.

### Related Topics

{% embed url="https://kb.heathenengineering.com/assets/physkit/components/force-effect-source" %}

{% embed url="https://kb.heathenengineering.com/assets/physkit/components/force-effect-reciever" %}

## Custom Effects

The Force Effect system was designed to be high customizable. You can create your own unique types of Force Effects by creating a script that that derives from the ForceEffect calss.

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
