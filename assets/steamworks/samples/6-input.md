# 6 Input

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of Steam Input API

![](<../../../.gitbook/assets/image (170) (1) (1) (1).png>)

It is important to understand what Steam Input is and how to properly configure it for your game.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/steam_controller" %}

You must configure your app to use Steam Input and you must use Valve's concept of an "In-Game Action" (IGA) file to define the action sets, action set layers and actions your game has.

{% embed url="https://partner.steamgames.com/doc/features/steam_controller/iga_file" %}

The Input tools provided by Heathen handle the integration with Steam Input in that you can define your sets, layers and actions as part of your Steam Settings object and easily activate them, fetch glyph data for them and of course query there state.

Heathen's tools take Valve's input system a step further and wrap all actions as [GameEvents](../../system-core/game-events.md) meaning you can handle Steam Input in a loop similar to traditional UnityEngine.Input or you as events similar to Unity's newer Input System.

### What do I learn?

1. Using steam's [Input](../api/input.md) API to handle controller input
2. Using [Input](../api/input.md) API to get button images and names
3. Using the [InputActionSet](../objects/input-action-set.md), [InputActionSetLayer ](../objects/input-action-set-layer.md)and [InputAction ](../objects/input-action.md)objects
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

### Instructions

#### To Test Input

1. Make sure you have Steam Client started and logged into a valid Steam user
2. Run the simulation
3.  Observe the note in the window, you should see various actions listed

    If you see No Controller Found&#x20;

    1. Insure you have a compatable controller active (XBox, Steam or PlayStation)
    2.  Insure Steam's Input API has been forced to your app by running

        [steam://forceinputappid/480](steam://forceinputappid/480)
4. With the session running and actions loaded operate the controller to see the values change.

{% hint style="warning" %}
The force input app ID command which can be ran from a browser should force Steam client to use input bindings for app 480.



The sample scene should clear this when it exits however if you find your Steam Input bindings are stuck on App 480 (Spacewars) you can run the command

[steam://forceinputappid/0](steam://forceinputappid/0) to force it to clear&#x20;
{% endhint %}

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### Controls UI

The controls UI uses standard Unity scripts and the [Input Action Glyph](../components/input-action-glyph.md) and [Input Action Name](../components/input-action-name.md) components to display the controls and mapped buttons to the user.

### DEMO SCRIPTS

The demo script for this scene operates the Steam Input API by reading data from the attached [InputAction](../objects/input-action.md) objects and controls the active action set and layer by using the attached [InputActionSet](../objects/input-action-set.md) and [InputActionSetLayer ](../objects/input-action-set-layer.md)objects.&#x20;

