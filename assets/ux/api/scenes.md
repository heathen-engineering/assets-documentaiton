---
description: Advanced scene management made easy
---

# Scenes

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../steam/steam.md">steam.md</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public static class API.Scenes
```

Did you know Unity can manage multiple scenes at once?

Want to learn more about multi-scene architectures? read this

{% embed url="https://kb.heathenengineering.com/company/concepts/multi-scene-architecture" %}

The Scenes interface makes working with multiple scenes simple and straitforward and provides useful tools and events making it trivial to set up loading notifications, page loaders and more.

### What can it do?

* Single line call to load and unload multiple scenes at once
* Iterate over available scenes and loaded scenes
* We handle the coroutines and activations for you
* Start, Update and Completed events and componenets make it easy to connect to your UI and other game systems.

## Events

### Started

```csharp
API.Scenes.EventStarted;
```

Invoked when a process is started. The provided paramiters will indicate what scenes are changing and in what way and progress for load, unload and overall will be reported.

### Updated

```
API.Scenes.EventUpdated;
```

Invoked on each frame of progress during an operation and indicates what scenes are being effected and how as well as the progress for unload, load and total progress.

### Completed

```
API.Scenes.EventCompleted;
```

Invoked when a process completes and indicates what scenes where effected.

## How To

### Get the available scenes&#x20;

This will return an array of the Scenes available to the system. Typically this is not needed however in mod supported games the collection of scenes that are available may change at runtime compared to development time.

```csharp
var scenes = API.Scenes.AvailableScenes;
```

This returns all scenes known by the system rather or not they are currently loaded. To fetch only the array of scenes that are currently loaded you can use

```csharp
var loadedScenes = API.Scenes.LoadedScenes;
```

### Check if a scene is loaded

In multi-scene games various systems can effect what scenes are loaded and unloaded when. It then offten becomes useful to test if a given scene is currently loaded or not.

```csharp
if(API.Scenes.IsSceneLoaded(scene));
```

You can test by scene build index or the name of the scene.

### Set Scene Active

Unity only ever has 1 scene active at a time, the active scene dicates which lighting environment is used. You can set a given scene active at any time via

```csharp
API.Scenes.SetSceenActive(scene);
```

### Transition between scenes

Unique to Heathen's system is the ability to transition between batches of scenes all at once. That is you can instruct the system to unload multiple scenes at the same time it is loading mutliple scenes and indicate which loaded scene you wish to make active if any.&#x20;

{% hint style="info" %}
Transition operations take a callback paramiter which is invoked every update frame and indicate the progress of the operation.
{% endhint %}

```csharp
API.Scenes.Transition(componenet, from, to, setActive, callback);
```

The transition operation has mutliple overloads to offer you the most efficent and simplest 1 line call possible for you given use case. You will notice that all Transition operations include a MonoBehaviour paramiter, this is used to manage the internal UnityEngine.SceneManager and its coroutines. You can pass any MonoBehaviour into this call so long as its not being unloaded :smile:

### Additive Load / Unload

You can add and remove scenes from the set of loaded scenes at anytime using the Load and Unload operations. These have the same requirements as the Transition operation in that they do requrie you pass in a MonoBehaviour reference.

```csharp
API.Scenes.Load(componenet, scene, callback);
```

```csharp
API.Scenes.Unload(componenet, scenes, callback);
```
