---
description: >-
  An open-source framework for working with Scriptable Object based variables
  and events.
---

# System Core

{% hint style="info" %}
The System Core articles are a work in progress and being updated frequently. If you have any questions at all please reach out over [Discord](https://discord.gg/6X3xrRc)
{% endhint %}

{% embed url="https://discord.gg/6X3xrRc" %}

{% hint style="success" %}
Heathen Engineering's _System Core_ is **open sourced** under the [MIT license](https://opensource.org/licenses/mit-license.php). You can find the source code for _System Core_ on [GitHub](https://github.com/heathen-engineering/Heathen-System-Core) ([https://github.com/heathen-engineering/Heathen-System-Core](https://github.com/heathen-engineering/Heathen-System-Core)), along with installation instructions and details on this licnese.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sub-license, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
{% endhint %}

{% embed url="https://github.com/heathen-engineering/Heathen-System-Core" %}

## Introduction

Heathen Engineering’s System Core is based on Unity’s Scriptable Object inspired by concepts discussed at Unit 2017 by Ryan Hipple.

{% embed url="https://www.youtube.com/watch?v=raQ3iHhE_Kk" %}

The framework defines the concepts of **Game Events** and **Scriptable Variables** which are derived from Unity’s Scriptable Object. This allows the designer to create data points and events as assets in the project’s asset database. The framework’s base classes can be easily expanded to create more complex data points, for example you could create your player profile as a serializable class or structure and use that with System Core to create a Scriptable Variable that represents your Player Profile, which can be easily serialized to a file/disk, which can raise an event on change and which can be easily referenced across scenes without needing the use of a singleton system.

## Installation

Heathen Engineering's System Core is available on Git&#x20;

{% embed url="https://github.com/heathen-engineering/Heathen-System-Core" %}

You can install Heathen Engineering's System Core from Git via Unity's Package Manager or via the Unity Package found in Git Releases section or via the Unity Asset store.

{% hint style="warning" %}
Note that Unity Asset store is maintained primarily to help user's discover the system. It is generally a few versions behind the Git repo as Unity must review and approve the asset before it can be listed.

Also be aware that all Heathen Assets include the framework. It is generally recommended to install System Core from the Unity Package listed on the Git Release page or via other Heathen Assets such as [Steamworks Complete](../steamworks/).
{% endhint %}

### Unity Package

1. Download the latest package from the release section on git\
   [https://github.com/heathen-engineering/Heathen-System-Core/releases](https://github.com/heathen-engineering/Heathen-System-Core/releases)
2. Import the package into your Unity Project

### Package Manager

1. Open the package manager and click the '+' (plus) button located in the upper left of the window
2. Select `Add package from git URL...` when prompted provide the following URL:\
   `https://github.com/heathen-engineering/Heathen-System-Core.git?path=\UnityPackage`
