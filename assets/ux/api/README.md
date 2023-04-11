---
description: Getting to know the UX API
---

# API

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

The UX API provides low level access to all of Heathen UX's features. API's members are all static classes and are used by higher level game object componenets to deliver the funcitonality of Heathen's UX. The UX API can be used to access features and funcitons of UX without the need of a GameObject reference and can be used to create tailor made systems and managers for your projects.

## Features

### Simple yet powerful

Clean simple, approchable static methods make most tasks a 1 liner

```csharp
API.Cursors.SetState(state);
```

```csharp
API.Windows.Focused.Maximize();
```

```csharp
API.Log.SaveToTextFile(fileName);
```

### Unity Native

Heathen's APIs are built with the Unity developer and programmer in mind. We make use of UnityEvents, Actions, ScriptableObjects and other standard Unity concepts and styles throughout the API.&#x20;

Where nessisary the Heathen API handles the various options in Unity, for example API.Cursors and API.Windows is comptable with both the old and new Unity Input systems and automatically uses the appropreate option.
