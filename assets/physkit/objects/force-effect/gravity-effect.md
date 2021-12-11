# Gravity Effect

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

A simple effect linear only effect which applies its force using the gravity formula.

AddForce(direction \* mass);

You can configure this effect to disable body gravity ... this mean that any body effected by this effect will have its Rigidbody.UseGravity set to false.

## Angular

No angular effect.

## Linear

Applies strength \* mass in the direction of the source.
