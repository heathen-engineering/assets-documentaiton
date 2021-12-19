# Buoyant Body

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

![](<../../../.gitbook/assets/image (159) (1).png>)

Used with the Surface Tool componenet to simulate the effect of buoyancy on a rigidbody.

### Fields and Attributes

### Buoyany Magnitude

Effectivly the gravity applied to the buoyant body, the force of buoyancy is the inverse of this value multiplied by the volume of the subject which is submerged below the surface.&#x20;

### Active Surface

A reference to the active [Surface Tool](surface-tool.md) this is used to find the surface level and density of the environment the subject is floating in.

### Calculation Mode

The [CalculationMode ](../enums/calculation-mode.md)to use when simulating the upward force.&#x20;

* Fast\
  A basic bounding volume based clacualtion&#x20;
* Simple\
  Same as fast but adds an additional calculation to self right the floating subject
* Complex\
  Uses the Physics Data hull and volume information to simualte buoyant force per vertex

### Submerged Ratio

The percentage of the attached [Physics Data](physics-data.md) that is submerged under the active surface tool and thus applying a buoyant force.
