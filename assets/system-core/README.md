---
description: >-
  An open-source framework for working with Scriptable Object based variables
  and events.
---

# System Core

{% embed url="https://github.com/heathen-engineering/SystemCore" %}

## Introduction

Heathen Engineering’s System Core is based on Unity’s Scriptable Object inspired by concepts discussed at Unit 2017 by Ryan Hipple.

{% embed url="https://www.youtube.com/watch?v=raQ3iHhE_Kk" %}

The framework defines the concepts of **Game Events** and **Scriptable Variables** which are derived from Unity’s Scriptable Object. This allows the designer to create data points and events as assets in the project’s asset database. The framework’s base classes can be easily expanded to create more complex data points, for example you could create your player profile as a serializable class or structure and use that with System Core to create a Scriptable Variable that represents your Player Profile, which can be easily serialized to a file/disk, which can raise an event on change and which can be easily referenced across scenes without needing the use of a singleton system.

