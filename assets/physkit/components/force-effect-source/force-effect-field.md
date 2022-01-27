# Force Effect Field

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (163) (1) (1).png>)

Applies a [Force Effect](../../objects/force-effect/) either as a global effect or as a triggered effect. One or more effects can be added and will be applied to any [Force Effect Reciever](../force-effect-reciever.md) that is effected by this field.

Force Effect Fields act as a sphere of influence for the given [Force Effect](../../objects/force-effect/) and when non-global discribe the falloff of the effect as a distance from the origin.

## Trigger

You would typically use a Sphere Collider set to trigger with Force Effect Field objects that are non-global.
