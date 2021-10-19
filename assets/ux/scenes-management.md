---
description: >-
  Explore the features and capabilities of User eXperience's Scenes system
  including multiscene management, batch load and unload and much more.
---

# Scene Manager Tools

## Introduction

The Scenes object helps you manage multi-scene, additive scene game architecture patterns. Multi-scene and additive scene paradigms can significantly improve performance and give you the developer a lot more flexibility in terms of design and architecture decisions; that is it allows you to group your scenes with respect to your games use as opposed to a single scene system where each scene exists on its own in isolation, and as a result must be a large monolithic structure which is slow to load and cumbersome to manage.

{% embed url="https://docs.unity3d.com/Manual/MultiSceneEditing.html" %}

### Why Though?

#### Efficency

* More, and smaller scenes are faster to load, easier to unload and offer more granularity in control of what you have loaded, and when. \
  Compared to having a few large scenes which take longer to load and have to be loaded in the entirety before use.\

* Common objects that would appear in all scenes can be defined once in one scene that simply persists. \
  Compared to having each individual scene defining these same objects further increasing the work that Unity must do to load initialize and eventually unload a given scene.

#### Maintainability

* Scenes can be broken up by geographic area in your game, state of the game world or even by function e.g. an environmental set of scenes, a UI/HUD scene, etc. meaning you can load into the editor and work on only the subset of objects relevant to you and your task at the moment.\
  Compared to having a monolithic scene that has everything in it. Slower to load, slower to save, harder to find specific objects needing more use of organizational objects (empty GameObjects acting like folders)\

* Reduce duplication, why should every scene have a camera, HUD, input system, event system, etc. Define these once in a scene that persists as needed.\
  Compared to every scene having its own copy, meaning a change to say camera FOV must now be applied to every scene exponentially increasing your workload and increasing the likelihood you forget one introducing bugs that aren't easy to detect as they don't throw errors.

#### Design Time Organization

* Breaking up objects across scenes by completed objects away from WIP (work in progress) scenes can help reduce the cost of on going development by reducing the likelihood of introducing bugs into previously completed work. The idea here is your WIP objects that are actively being worked on live in there  own scene so changes to them do not unintentionally impact completed objects in other scenes.\
  Compared to a monolithic scene structure its all to common to unintentionally change a structure or disable something for testing of some WIP object, forgetting you did so and that bug slipping through unnoticed for a prolonged period of time causing run on issues in later development.\

* When working in a team collaboration is always a point of challenge. Splitting scenes apart based on work delegation can reduce conflicts and greatly simplify change management. This can be coupled with WIP (work in progress) scenes enabling parallel development while minimizing the complexities typical in such cases.\
  Compared to a monolithic scene structure where very often work must be stopped by some team members while others finish some change. A Unity scene is a single file after all and simultaneous collaboration on a single scene is a challenge even for a vetted engineering team.

### Concept

Often, and the name of the thing reinforces this notion; we as developers think of a "scene" as a physical area in our game, similar to a stage where our actors can play. This notion however is rather limiting and not at all true with regards to what a scene is in terms of the Unity Engine.‌

A scene is more accurately thought of as a folder or collection of GameObjects. How you choose to break your "scenes" up should not typically be based on physical local as much as it should be based on load order. To put that in a different context; when are these things of use to have in memory, that is when they should be loaded and when they are no longer of use that is when they should be unloaded.‌

To determine what should be loaded when we need to understand the concept of "Scope", that is we should load all the objects that are "in scope" or are expected to be "in scope" soon and unload any objects that are "out of scope".

### Determining Scope

#### Physical Location

One obvious way to determine the relevant scope of an object to load is its physical location. This though is only really relevant for things that do not move.  Things where the player moves closer to or further away from the object thus bringing the object into or out of scope.

{% hint style="info" %}
You will often see the term "Page" or "Pages" to refer to collections of objects defined by location, the idea being the player is on a page and we load that page and the 8 other adjacent pages.

A more natural term might be "tile" like the tiles on a floor. You are at any given time standing on 1 tile. You are likely to move to one of the adjacent tiles (8 possible options in most worlds) so this system gives us an easy way to determine what "pages" e.g. what scenes we should consider "in scope" and thus load.
{% endhint %}

This approach of local based scope does not apply to MOBs (literally stands for Mobile Object) as these objects can move them selves in or out of scope. They can for example chase the player across many "pages" or scenes and so loading them in or unloading them based on some location would cause them to pop out of existence as they chased the player. The player its self is another example of such a mobile object. For MOBs we would want to handle them in a scene that is persistent e.g. loads with the start of the session and unloads with the end of the session.

#### By Use

Most objects wont be loaded based on location but rather based on use. For example regardless of physical location there are some objects we just always need in memory and these we want to load at the start of the game and never unload, e.g., bootstrap objects such as:

* The camera
* The Audio Listener
* The Event System
* The Input System
* Game systems such as&#x20;
  * Network Managers
  * Steamworks Behaviors
  * etc.

The above are objects that are always present but there are also objects that are persistent through various phases of the game, again regardless of the physical location of the player for example the HUD or GUI the player uses during gameplay would be persistent regardless of location but wouldn't be in scope while the player is in the main menu.

#### By Context

Depending on your game there may be more context specific factors to consider when loading or unloading a scene. A simple example might be a game where a player may choose to burn down a forest for example. You could define this area as a single page and handle the forest being burnt or not as a run time process, but this would use clock time unnecessarily. A simpler approach would be to have 2 scenes, 1 for the unburnt forest and 1 for the burnt one. Now your processing is as simple as which should be loaded.&#x20;

## Scenes

This is a component to be added on a game object typically in your [bootstrap scene](../../company/concepts/bootstrap-scene.md). It will be responsible for managing the asynchronous load and unload of scenes. This component exposes a number of events that can be used to drive features such as loading screens.

![](<../../.gitbook/assets/image (78).png>)

{% hint style="info" %}
You will see the term Bootstrap or Bootstrap Scene used in this and other documents. You can read more on that concept [here](../../company/concepts/bootstrap-scene.md). Note that the first scene in your game is by definition your bootstrap scene e.g. build index 0 is bootstrap.
{% endhint %}

#### References

{% hint style="info" %}
#### Game Events

_**System Core and thus Game Events are included with UX**_

A [Game Event](../system-core/game-events.md) is a special type of Scriptable Object that works much like a Unity Event but is defined as part of your game (in your asset folder) and thus always available. In contrast a Unity Event is defined as part of a component on a Game Object and is only available while that object exists in memory.

To learn more see [Heathen Engineering's System Core documentation](../system-core/).
{% endhint %}

The Scenes Manager has three (3) optional references being the&#x20;

* Started\
  This is a [Game Event](../system-core/game-events.md) that will be invoked when a scene process has started
* Updated\
  This is a [Game Event](../system-core/game-events.md) that will be invoked when a scene process has updated
* Completed\
  This is a [Game Event](../system-core/game-events.md) that will be invoked when a scene process has completed

#### Events

The Scenes Manager has three (3) Unity Events exposed

* Evt Started\
  Invoked when a process has started
* Evt Updated\
  Invoked when a process has updated
* Evt Completed\
  Invoked when a process has completed

## Examples

{% hint style="success" %}
The following examples work with the build index of scenes. Due to limitations with Unity's Scene Manager it's recommended to use the build index version of each method.

Variations of each method are available to work with scene name. These variations cannot perform validation logic and will not populate the SceneProcessState load list and unload list.
{% endhint %}

### Load a scene

| Paramiter | Type                       | Use                                                                               |
| --------- | -------------------------- | --------------------------------------------------------------------------------- |
| scene     | int                        | The index of the scene to be loaded.                                              |
| setActive | bool                       | Should the loaded scene be set active on load?                                    |
| callback  | Action\<SceneProcessState> | An action to be invoked at the start, on update and on completion of the process. |

```csharp
Scenes.Load(sceneIndex, setActive, callback);
```

### Load multiple scenes

When working in a multi-scene game its often that you want to load multiple scenes at once and need to know when all are ready or if any had an issue. This is the core feature provided by Heathen's Scenes object.

| Paramiter   | Type                       | Use                                                                               |
| ----------- | -------------------------- | --------------------------------------------------------------------------------- |
| scene       | List\<int>                 | The index of each scene to be loaded                                              |
| activeScene | int                        | The index of the scene to set active                                              |
| callback    | Action\<SceneProcessState> | An action to be invoked at the start, on update and on completion of the process. |

```csharp
var scenes = new int[] { 1, 4, 2};
Scenes.Load(scenes, 4, callback);
```

### Unload a scene

| Parameter | Type                       | Use                                                                               |
| --------- | -------------------------- | --------------------------------------------------------------------------------- |
| scene     | int                        | The index of the scene to be unloaded.                                            |
| callback  | Action\<SceneProcessState> | An action to be invoked at the start, on update and on completion of the process. |

```csharp
Scenes.Unload(sceneIndex, callback);
```

### Unload multiple scenes

| Parameter | Type                       | Use                                                                               |
| --------- | -------------------------- | --------------------------------------------------------------------------------- |
| scene     | List\<int>                 | The index of the scenes to be unloaded.                                           |
| callback  | Action\<SceneProcessState> | An action to be invoked at the start, on update and on completion of the process. |

```csharp
var scenes = new int[] { 1, 4, 2};
Scenes.Unload(scenes, callback);
```

### Transition between scenes

This loads in a set of scenes and unloads the other set. Its functionally the same as calling Load on scenes and Unload on scenes at the same time.

| Parameter   | Type                       | Use                                                                               |
| ----------- | -------------------------- | --------------------------------------------------------------------------------- |
| from        | int                        | The index of the scene to be unloaded.                                            |
| to          | int                        | The index of the scene to be loaded                                               |
| setToActive | bool                       | Should the newly loaded scene be set active                                       |
| callback    | Action\<SceneProcessState> | An action to be invoked at the start, on update and on completion of the process. |

```csharp
Scenes.Transition(1, 2, true, callback);
```

### Transition between multiple scenes

This unloads a set of scenes while loading another set of scenes

| Parameter   | Type                       | Use                                                                               |
| ----------- | -------------------------- | --------------------------------------------------------------------------------- |
| from        | List\<int>                 | The index of the scenes to be unloaded.                                           |
| to          | List\<int>                 | The index of the scenes to be loaded                                              |
| activeScene | int                        | The index of the scene to make active                                             |
| callback    | Action\<SceneProcessState> | An action to be invoked at the start, on update and on completion of the process. |

```csharp
var toUnload = new int[] { 1, 4, 2};
var toLoad = new int[] { 3, 5, 6};
Scenes.Transition(toUnload, toLoad, 5, callback);
```

### Callbacks

You will notice that all process calls have a callback parameter. This callback parameter is an action that will be invoked by the process at each state of the process and will send as a parameter the SceneProcessState state object.

#### Scene Process State

| Attribute          | Data Type  | Usage                                                                                                                                                                               |
| ------------------ | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| setActiveScene     | int        | <p>Indicates the scene to be set active at the end of the process.</p><p>A value &#x3C; 0 indicates no scene should be set active.</p>                                              |
| unloadTargets      | List\<int> | <p>The list of scenes to be unloaded. <br>Scenes will be unloaded in parallel, e.g. all at once.</p>                                                                                |
| loadTargets        | List\<int> | <p>The list of scenes to be loaded. </p><p>Scenes will be loaded in parallel, e.g. all at once.</p>                                                                                 |
| unloadProgress     | float      | A value between 0 and 1 indicating the progress of unloading all target scenes                                                                                                      |
| loadProgress       | float      | A value between 0 and 1 indicating the progress of loading all target scenes                                                                                                        |
| transitionProgress | float      | A value between 0 and 1 indicating the overall progress of the process                                                                                                              |
| complete           | bool       | <p>True when the process is complete.</p><p>This will be set true on completion rather or not there is an error</p>                                                                 |
| hasError           | bool       | True when an error has occurred                                                                                                                                                     |
| errorMessage       | string     | <p>A string indicating the errors that occurred.</p><p>Conditions are validated before any action is started so if an error occurs it will prevent any action from being taken.</p> |

{% hint style="warning" %}
The callback is called at the start of the process, on every update (usually once a frame) and at the end of the process.
{% endhint %}

The following example code simply demonstrates accessing the members of the SceneProcessState. If you created a method such as this it would be provided as the final parameter on a call such as Load ... for example

```csharp
Scenes.Load(2, true, HandleUpdate);
```

{% hint style="info" %}
Note that the complete field is always set true when the process has completed rather or not it has an error. The process should be treated as in progress until complete is true and you should check if "hasError" even if "complete" is true.&#x20;

Complete simply means that the process finished working, it does not indicate success or failure.
{% endhint %}

```csharp
private void HandleUpdate(SceneProcessState state)
{
    if(state.complete)
    {
        //Complete indicates that the process is finished
        //If this is false then the process is still running
    }

    if(state.hasError)
    {
        //Has Error indicates that some error was encountered
        //You can get a string message as to what happened via state.errorMessage
        Debug.LogError(state.errorMessage);
    }

    Debug.Log("Load Progress: " + state.loadProgress.ToString("P1"));
    Debug.Log("Unload Progress: " + state.unloadProgress.ToString("P1"));
    Debug.Log("Total Progress: " + state.transitionProgress.ToString("P1"));
}
```

A more common use case is to use an anonymous method via expression.

```csharp
Scenes.Load(2, true, (state) =>
    {
        if(state.complete)
        {
            Debug.Log("Load is done.");
            
            if(state.hasError)
            {
                Debug.LogError("The load has errors: " + state.errorMessage);
            }
        }
        else
        {
            Debug.Log("Load: " + state.loadProgress.ToString("P1")
                + "\nUnload: " + state.unloadProgress.ToString("P1")
                + "\nTotal: " + state.transitiionProgress.ToString("P1"));
        }
    });
```

