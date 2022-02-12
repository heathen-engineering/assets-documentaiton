# Force Effect Source



{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

A Force Effect Source is a simple component behavior that describes the origin of a Force Effect. Two main types of Force Effect Sources are provided and described in the articles below.

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
