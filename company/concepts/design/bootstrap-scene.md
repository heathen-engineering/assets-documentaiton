---
description: Understanding the concept of a boostrap scene in Unity
---

# 🥾 Bootstraping

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
#### Definition

_**Bootstrap**_\
_Noun_\
**COMPUTING** a technique of loading a program into a computer by means of a few initial instructions which enable the introduction of the rest of the program from an input device.

_Verb_\
**COMPUTING** fuller form of boot. "boot" such as to "boot" your PC is a short form of "bootstrap"
{% endhint %}

A Bootstrap scene is where we define a simple scene containing only the system level objects of our game. The purpose is to initialize the core systems of a game, to validate the environment and systems are ready to load the game and then to load the main game.

{% embed url="https://www.youtube.com/watch?v=rDNOpask9mQ" %}

{% embed url="https://github.com/heathen-engineering/Examples/tree/main/UnityProjects/Bootstrap%20Scene%20Example%20Project" %}
Bootstrap Scene Example Project
{% endembed %}

## Reasoning

### Do Not Destroy On Load

While you can use Do Not Destroy On Load with the content of a Bootstrap scene, it's not sufficient to apply Do Not Destroy On Load to objects in a scene that is loaded multiple times, such as a title or main menu scene.

{% hint style="warning" %}
Why?\
Reloading data that is already in memory is a waste of time and increases the chance of an error due to more data and more "moving parts".&#x20;



Know that when you reload a scene that had marked some object Do Not Destroy On Load for a moment there is duplicate data in memory, Unity will need to identify the objects by ID and remove the duplicates. In some cases that fact can make a big mess especially when regarding unmanaged memory or multi-process systems, like Steam API and many networking tools.
{% endhint %}

As such you are advised to put your system level objects in a bootstrap scene, which should be on build index 0 and only ever loaded once. This is whether or not you use Do Not Destroy On Load.

### Stand Alone Scenes

A common argument is that every scene should be standalone, that is that every scene should be able to be loaded on its own and function without error. The usual argument is that this makes development and unit testing easier in that you can load any scene at any time and play test it without concern of other factors.

{% hint style="success" %}
Did you know Unity Editor can have multiple scenes loaded at once? You can define a Bootstrapper scene and leave it loaded at all times simply swapping out what other scene may be loaded, thus giving you the very same development time capabilities as if every scene had defined every dependency.

In this model you use multi-scene additive loaded as opposed to the older single scene approach where on load previous the previous scene is unloaded. This gives greater control and avoids the need to use Do Not Destroy On Load, removes the cost of auto unload which is often a slow process in Unity and allows you to load any scene at any time knowing that because the bootstrap scene is already loaded that its dependents such as cameras are already loaded.
{% endhint %}

If you think about the concept of every scene being standalone, what you are saying is that every scene must define and initialize all required/dependent systems on load. There are always various systems in a game that are simply globally scoped that is must be present for the game to work, and so every one of your scenes in this model must define them and initialize them

* Main Camera
* Audio Listener
* Input Handler / Event System

The above three are the bare bones for rendering, handling input and playing audio. Most games will have several others such as:

* Error handler\
  A UI used to express errors to the user for a more graceful shutdown in the event of fatal error
* Loading screen\
  A UI or presentation used to mask changes to the world space during load and unload operations
* System Managers\
  Any global systems a game uses such as Steam API, Networking Managers, game systems such as ORK, etc.
* Validation Tools\
  Often overlooked or perhaps you consider it part of Error handler, the idea is a system tool that checks for the integrity of the dependent systems used by the game. This enables graceful failure as opposed to the all to often seen hard crash to desktop.

More over on change of scenes the game must load the new one in creating a duplicate and destroy the old scenes copy momentarily doubling the memory and processing requirement for said objects.

### Multi-scene Additive Loading

This is the method Heathen Engineering uses and recommends for most if not all use cases. The idea is simple enough. You simply never unload your bootstrap scene and when you load scenes you do so as additive loading handling unloading of scenes you no longer need your self

{% embed url="https://docs.unity3d.com/ScriptReference/SceneManagement.LoadSceneMode.Additive.html" %}

{% embed url="https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.UnloadSceneAsync.html" %}

Heathen Engineering's UX Asset provides tools to help you manage multi-scene structures, and even batch loading and unloading of multiple scenes at once, however you can do this easily on your own with Unity's SceneManagement tools.

The advantage to this approach is that you have full control of load and unload, unload being a typically costly operation in Unity.&#x20;

As an example if we defined a bootstrap scene and marked its objects as Do Not Destroy, then used a non additive load to load the title, then Unity would iterate over every object defined by the bootstrap scene and check if it should be unloaded. This is slow but necessary as we could have, and did in this case, mark the objects as do not destroy on load.

In contrast if we simply load the title scene additive, we skip this depth-wise search of every object defined in the previous scene. But what about the load into the gameplay scene, we will want to unload the title scene as well.&#x20;

If you loaded the game scene without additive options, then before Unity activated the objects in the game scene it would first iterate over and unload the title scene leaving a period of time where the game was simply unresponsive.&#x20;

In contrast if you loaded the game scene additively you can choose to activate it before you unload the title scene. Typically this is what Heathen would do, we would:&#x20;

1. Show the loading screen\
   This is a feature of the bootstrap scene and thus always available and unaffected by any load or unload operation
2. We would disable the game objects of the title scene, we make this easy on our selves by storing them in a root object so we can simply disable 1 thing, but you can use whatever method works for you. Point is they are disabled e.g. not active but are still present
3. We load the game scene additively and activate it right away\
   At this point we can close out the loading screen and return control to the user as the game is now playable again.&#x20;
4. We asynchronously unload the title scene\
   This is optional, if your game returns to the title scene often it may actually be more useful to simply disable and re-enable it as opposed to load and unload it. The point is however that you can do this in the background while the player is getting on with playing the game. No need to make them wait for this to be done.

{% hint style="info" %}
If you have ever created a scene in Unity that creates a lot of objects at run time, you may have noticed that Unity takes a very long time unloading such a scene. This is due to Unity iterating over the objects.

You can speed this up by destroying objects yourself before unloading the scene, especially those objects you created at run time. If you simply spawn all such objects under some given root GameObject, yes that does add a layer to the transform hierarchy which can complicate transform operations, but it also means you can destroy all such objects with a single Destroy command so test various options and see what gives you the best results for your game.

The point here is do not simply rely on Unity's Load and Unload to be the best option for your game. Manually controlling memory is not as hard as you might think and can open a lot of possibilities to you.
{% endhint %}

## Architecture

![](<../../../.gitbook/assets/image (74) (1).png>)

The above diagram shows the basic flow from 1 scene to another.&#x20;

{% hint style="info" %}
The flow demonstrated above works for both additive and single scene architectures
{% endhint %}

### Bootstrap

When the user "bootstraps" aka "boots" the game we enter the "bootstrap" scene. This scene typically defines the following objects and components

| Game Object           | Component                                                                               | Reason                                                                                                                                                                                                                                              |
| --------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Main Camera           | [Camera](https://docs.unity3d.com/ScriptReference/Camera.html)                          | <p>Renders objects to the output screen.</p><p>This is required to render.</p>                                                                                                                                                                      |
|                       | [Cinemachine Brain](https://unity.com/unity/features/editor/art-and-design/cinemachine) | <p>This allows the use of Cinemachine Virtual Cameras <br>This is the default standard for modern Unity games.</p>                                                                                                                                  |
|                       | [Audio Listener](https://docs.unity3d.com/ScriptReference/AudioListener.html)           | <p>This functions as the listening point for audio sources</p><p>This is required to have audio play.</p>                                                                                                                                           |
| Event System          | Depends on Unity Version                                                                | <p>This may be Event System (2018) <br>and or Input Modules (2018 and later)</p><p>Handles user input and UI events</p>                                                                                                                             |
| Splash/Loading Canvas | Canvas                                                                                  | <p>A UnityEngine.UI.Canvas or similar UI root</p><p>This would be the root of a splash screen UI if any</p><p>This is used as a loading cover at the start and </p><p>at any other point needed by the game such as </p><p>between scene loads.</p> |
| Error Dialog          | Canvas                                                                                  | <p>A UnityEngine.UI.Canvas or similar UI root</p><p>This would be the root of a error dialog UI</p><p>Every game should have an error dialog</p><p>Error dialog should be the top most UI canvas</p>                                                |
| Validator             | Script you write                                                                        | <p>This is a component you create <br>it should validate the needs of your game e.g. <br>accounts logged in, system meets min specs, user has</p><p>a license, systems have initialized, etc.</p>                                                   |
| System Managers       | <p>SteamworksBehaviour</p><p>Mirror.NetworkManager</p><p>ORK</p><p>etc.</p>             | <p>This is the object you place your various system </p><p>managers on. What managers you have will vary <br>depending on your game's needs</p>                                                                                                     |

If you are using additive loading you would simply never unload this scene and you would have the validator additively load the title scene when all was found to be ready.

If you are using the older single scene structure you would mark all objects as "Do Not Destroy On Load" or simply nest them all under a common Game Object and mark it as Do Not Destroy On Load. This will cause Unity to create a hidden scene and move all objects to that hidden scene. You can then have the validator when ready call Load on the title scene thus causing the bootstrap scene to unload.

#### Main Camera

Notice that we have defined the Main Camera and its various parts here in the bootstrap. This means that we do not need to define and should not define a camera in the other scenes. It is recommended that you use Cinemachine and its Virtual Cameras in all other scenes they will automatically drive the main camera for you via the Cinemachine Brain and in fact this is the default set up in new HDRP scene templates.

#### Splash Canvas

You will also note the inclusion of the Splash at the start. This UI would normal be enabled at dev time thus enabled at the start. It can initially present your company logo or other "splash screen" like information, and later be used as a loading screen or similar transitional UI between sections of your game. Because its present here in the bootstrap you know its always available. We usually drive this UI via a Static or singleton model. In most cases you would want to avoid a singleton however this is a case where there is truly only ever one instance and it is truly always available.

#### Error Dialog&#x20;

Next we have the Error Dialog. This is a UI canvas that should always render over the top of and block the IO for all other canvas. Its purpose is to provide the user with system level error information, which shouldn't ever happen but likely will. This insures that when your game encounters a fatal error it can notify the user in a meaningful way and exit nicely.

This would be where you handle bug reporting, feedback, etc. all of which are features provided by Heathen's UX SDK. Rather or not you use Heathen's UX you really should still have an Error Dialog.

#### Validator

This is a bespoke (custom written by you) component that should handle validating the system, environment and game before trying to load. This is how you catch fatal errors before you encounter a hard crash to desktop, at least as much as is possible. A bare bones example would be a simply script that listens for SteamworksBehaviour's initialization event, and if successful loads the title and if not notifies the user of the issue and closes gracefully.

A properly formed validation layer and error notification system such as Error Dialog and Feedback system is key to professional software game or otherwise.

#### System Managers

This will vary depending on your game, but would include components such as Steamworks Behavior, Mirror's Network Manager and other system level managers and controllers. That is things that should load at the start and persist throughout the game. The Validator will work with these system managers to know when the game is ready to fully load and if something went horribly wrong, such that you need to notify the user and close gracefully.

### Title

The title scene is fairly self explanatory in most cases. This scene simply defines the main menu style UI, or whatever other initial entry point your game will be using. Follows are some concepts often seen in games, which your game uses is up to you. The point is, this is the first human interface point for your game. Calling it a "title" scene is just a habit, it doesn't have to present the title if that isn't relevant for your game.

* Start Menu\
  The old classic, this is where you very simply present a screen that says press start to play. Some platforms require you to have such a menu. This screen often contains legal information such as copy right and may present a passive scene, that is a scene with no human interaction. \
  Despite being so simple this is still your first point of human interaction, as by definition it requires the human to start before it transitions further
* Main Menu\
  Slightly more modern but still an old classic, this replaced the start screen in most PC games decades ago and is the UI that the Start Menu would navigate to when the user pressed start. This menu is the programs main menu, and typically had menu entries such as Play Game, Options, Exit, Credits, etc.
* Login\
  Most games these days silently login if they login at all, older games or games going for that traditional feel may use a Login UI as opposed to a Start Menu UI. MMOs often use this sort of structure.
* Dashboard\
  A more modern approach to the Main Menu, it's still fundamentally a Main Menu. The only notable difference is its less of a Menu and more of a HUD (Heads Up Display). This sort of UI might have many interaction points such as showing game news, social features, game store, profile data, statistics and of course the usual Main Menu fair of Play, Quit, etc.

No matter the structure you use, at some point the user will get to the stage of playing the actual game where you need to load one or more gameplay scenes. It is the title.scene in our diagram that handles that action and starts the load process of the gameplay scenes.

### Gameplay

This is a scene structure wholly unique to your game, the only relevant part here is that if your user exits the gameplay scenes they would be returning to the title.scene, not the bootstrap. Bootstrap is only ever loaded once at the start and never again.

## How To

The whole point of a bootstrap scene is that it validates the status of the environment before trying to load the game. Doing this in such a structured way as noted improves efficiency of your game greatly and allows for a much more graceful handling of any issues. Graceful handling is not just a matter of good user experience it also means you can report issues intelligently and thus it will be easier to handle them when they occur and they will occur.

The typical approach is to create a "bootstrapper" script that will live in your "bootstrap" scene. This script will be responsible for validating whatever it is you need to validate and handling the results of that validation.&#x20;

For a crude example:

{% hint style="success" %}
This example assumes you are using Steam and have some behaviour in your game called `ErrorController` and some static class or structure in your game called `GameSettings` the idea though should be clear no matter how you handle errors and settings.
{% endhint %}

{% hint style="warning" %}
This is a crude example and should not be copy and paste into your production game. \
This is meant to demonstrate the concept of validating an environment.
{% endhint %}

```csharp
public class Bootstrapper : MonoBehaviour
{
  public ErrorController errorController;
  public LoadingScreenController loadingScreen;

  void Start()
  {
    GameSettings.MainCamera = Camera.Main;
    GameSettings.ErrorController = errorController;
    GameSettings.LoadingScreen = loadingScreen;
    // ... whever ever else you have
  }

  void Update()
  {
    if(SteamSettings.HasInitalizationError)
    {
        errorController.ReportError("An error occured while initalizing Steam API, " 
        + "this is a required system and so the game must close. "
        + "If this persists please contact technical support."
        + "\n\nError Message: "
        + SteamSettings.InitalizationErrorMessage);
        Application.Quit();
    }
    else if (SteamSettings.Initialized)
    {
        //All is well so load the title scene
        StartCoroutine(LoadTitle());
    }
  }

  IEnumerator LoadTitle()
  {
    //This should load the title scene async and update UI to reflect status
    //This should handle any error in loading the title scene, 
    //report it to the user if it happens and close the app nicely
  }
}
```
