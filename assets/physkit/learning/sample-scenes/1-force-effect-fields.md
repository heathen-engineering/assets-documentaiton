# 1 Force Effect Fields

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (153).png>)

This scene serves as a simple playground for force effects. You'll find a simple UI on the left side letting you turn different force effect fields on and off. These fields are rotating around the room effecting the spheres in the room. In addition a wind effect direction is applied to room pushing subjects away from the camera.

## What do I Learn?

1. What is a [Force Effect](../../api/force-effects.md)
2. What is a [Force Effect Source](../../components/force-effect-source/)
3. What is a [Force Effect Reciever](../../components/force-effect-reciever.md)&#x20;
4. Differece between [Force Effect Field](../../components/force-effect-source/force-effect-field.md) and [Force Effect Direction](../../components/force-effect-source/force-effect-direction.md)

## Objects

### Weather Vane

A Force Effect Reciever responding only to the global wind effect.

### Wind Field Generator

This is actually a Force Effect Direction set to global and applying the Wind Effect to all recievers

### Pivot

The pivot game obejct simply rotates at a constnat rate, a child of this object are the 4 Force Effect Fields noted in the UI and represented as spheres rotating around the room.

### Balls

Each ball has a Force Effect Receiver attached&#x20;
