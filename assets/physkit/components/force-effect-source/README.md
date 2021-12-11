# Force Effect Source



{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

A Force Effect Source is a simple component behaviour that discribes the origin of a Force Effect. Two main types of Force Effect Soruces are provided and discribed in the articles below.

## Custom Source

The Force Effect system is highly customizable and extensable ... you can create a custom Force Effect Source by simply deriving from the ForceEffectSource behaviour.

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

The only requried feature is the AddForce method which takes 4 paramiters

### Subject

This is the [Physics Data](../physics-data.md) of the reciever a powerful feature that discribes all physical aspects of the subject

### Sinsativity

This discribes the sinsativity of the object to any effect and is a simple scalar e.g. 0 means you can ignore the effect any non-zero value should be used to scale the effect.

### Use Angular

Is the subject listening for angular effects, if false you should not operate the effects angular methods

### Use Linear

Is the subejct listening for linear effects, if false you should not operate the effects linear methods

## Custom Effect Tips

### Global

We offten want to apply an effect globally to all listeners that would have it. To do so we need to add the effect to the API.ForceEffect.GlobalEffects list ... and we need to remove the effect when its no longer applicable.

The approch Heathen uses is to expose an Is Global field

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
