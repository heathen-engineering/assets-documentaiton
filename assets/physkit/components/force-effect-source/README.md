# Force Effect Source

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

A Force Effect Source is a simple component behaviour that describes the origin of a Force Effect. Two main types of Force Effect Sources are provided and described in the articles below.

### Related Topics

{% embed url="https://kb.heathenengineering.com/assets/physkit/objects/force-effect" %}

{% embed url="https://kb.heathenengineering.com/assets/physkit/components/force-effect-reciever" %}

## Custom Source

The Force Effect system is highly customizable and extensible ... you can create a custom Force Effect Source by simply deriving from the ForceEffectSource behavior.

```csharp
public class CustomEffectSource : ForceEffectSource
{
    public override void AddForce(PhysicsData subject, 
                                  float sinsativity, 
                                  bool useAngular, 
                                  bool useLinear)
    {
        // Do Work
    }
}
```

The only required feature is the AddForce method which takes 4 parameters

### Subject

This is the [Physics Data](../physics-data.md) of the receiver a powerful feature that describes all physical aspects of the subject

### Sensitivity

This describes the sensitivity of the object to any effect and is a simple scalar e.g. 0 means you can ignore the effect any non-zero value should be used to scale the effect.

### Use Angular

Is the subject listening for angular effects, if false you should not operate the effects angular methods

### Use Linear

Is the subject listening for linear effects, if false you should not operate the effects linear methods

## Custom Effect Tips

### Global

We often want to apply an effect globally to all listeners that would have it. To do so we need to add the effect to the API.ForceEffect.GlobalEffects list ... and we need to remove the effect when its no longer applicable.

The approach Heathen uses is to expose an Is Global field

```csharp
[SerializeField]
private bool _isGlobal = false;
public bool IsGlobal {
    get { return _isGlobal; }
    set
    {
        if(value)
        {
            if(!API.ForceEffects.GlobalEffects.Contains(this))
                API.ForceEffects.GlobalEffects.Add(this);
        }
        else
        {
            if (API.ForceEffects.GlobalEffects.Contains(this))
                API.ForceEffects.GlobalEffects.Remove(this);
        }
    }
}
```

And to set the value on enable of the source

```csharp
private void OnEnable()
{            
    if (_isGlobal)
    {
        if (!API.ForceEffects.GlobalEffects.Contains(this))
            API.ForceEffects.GlobalEffects.Add(this);
    }
}
```

And remove it on disable

```csharp
private void OnDisable()
{
    API.ForceEffects.GlobalEffects.Remove(this);
}
```

## Effects

Which effects your custom source applies is up to you. Heathen's standard sources make this configurable, exposing a list of Force Effect to the editor and then simply iterating over those when AddForce is called.
