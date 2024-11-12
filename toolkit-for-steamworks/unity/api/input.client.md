---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Input.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using SteamInput = HeathenEngineering.SteamworksIntegration.API.Input.Client;
```

```csharp
public static class Input.Client;
```

### What can it do?

Steam Input API is a flexible action-based API that supports all major controller types - Xbox, Playstation, Nintendo Switch Pro, and Steam Controllers.

{% embed url="https://partner.steamgames.com/doc/features/steam_controller" %}

To learn more about Steam Input in Heathen's Steamworks Complete [read this article](../../../steam/input.md) on the core concept.

## Events

### Event Input Data Changed

When the Update method is ran and a controller has 1 or more input changes since its last test this event will raise and will carry with it information about the controller and all actions on it including all changes since the last update was ran.

```csharp
public static ControllerDataEvent EventInputDataChanged;
```

The handler would take the form of

```csharp
void HandleEvent(InputControllerData data)
{
    //Do Work
}
```

## Fields and Attributes

### Initialized

```csharp
public static bool Initialized => get;
```

Indicates rather or not the Seam Input API has been initialized. You must initialize the Steam Input API before it can be used. This is handled automatically for you if you have defined Inputs in the Steam Settings object.

### Controllers

```csharp
public static InputHandle_t[] Controllers => get;
```

Returns the array of controller handles currently connected to the game.

## Methods

### Add Input

Adds an input action to the list of tracted input actions, if your using a [SteamSettings ](../classes-and-structs/steam-settings/)object this will be done for you for all InputActions defined in the [SteamSettings](../classes-and-structs/steam-settings/). Once an action is added it can be updated by the API and tools such as the [SteamInputManager ](../components/steam-input-manager.md)can be used to track changes.

```csharp
public static void AddInput(string name, InputActionType type);
```

### Remove Input

Removes an input from the list of tracked inputs, its safe to try to remove and input that was not currently tracked.

```csharp
public static void RemoveInput(string name);
```

### Update

Updates the internal state of the indicated controller. Typically you would use the Steam Input Controller which would handle the update of each controller tracked.

```csharp
public static InputControllerData Update(InputHandle_t controller);
```

### Activate Action Set

Reconfigures the controller to use the specified action set (ie "Menu", "Walk", or "Drive").

This is cheap, and can be safely called repeatedly. It's often easier to repeatedly call it in your state loops, instead of trying to place it in all of your state transitions.

```csharp
API.Input.Client.ActivateActionSet(controller, actionSet);
```

### Activate Action Set Layer

Reconfigures the controller to use the specified action set layer.\
\
See the [Action Set Layers](https://partner.steamgames.com/doc/features/steam\_controller/action\_set\_layers) article for full details and an in-depth practical example.

```
API.Input.Client.ActivateActionSetLayer(controller, actionSet);
```

### Deactivate Action Set Layer

Reconfigures the controller to stop using the specified action set layer.

```csharp
API.Input.Client.DeactivateActionSetLayer(controller, actionSet);
```

### Get Active Action Sets

Fill an array with all of the currently active action set layers for a specified controller handle.

```csharp
var actionSets = API.Input.Client.GetActiveActionSetLayers(controller);
```

### Get Action Set Handle

Lookup the handle for an Action Set. Best to do this once on startup, and store the handles for all future API calls.

```csharp
var handle = API.Input.Client.GetActionSetHandle(setName);
```

### Get Action Data

Returns the action data for the indicated input action, this works for Input Actions that have been added to the Input API via the AddInput method.

The first option assumes the first controller in the list of available controllers

```csharp
public static InputActionData GetActionData(string name);
```

The second takes a controller as input and returns the data for that controller

```csharp
public static InputActionData GetActionData(InputHandle_t controller, string name);
```

### Get Analog Action Data

Returns the current state of the supplied analog game action.

```csharp
var data = API.Input.Client.GetAnalogActionData(controller, actionHandle);
```

### Get Analog Action Handle

Get the handle of the specified Analog action.

{% hint style="warning" %}
This function does not take an action set handle parameter. That means that each action in your VDF file must have a unique string identifier. In other words, if you use an action called "up" in two different action sets, this function will only ever return one of them and the other will be ignored.
{% endhint %}

```csharp
var handle = API.Input.Client.GetAnalogActionHandle(actionName);
```

### Get Analog Action Origins

Use this to display the appropriate on-screen prompt for the action.

```csharp
var origins = API.Input.Client.GetAnalogActionorigins(controller, 
                                actionSet, 
                                actionHandle);
```

### Get Connected Controllers

Returns the handles for the connected controllers

```csharp
var controllers = API.Input.Client.ConnectedControllers;
```

### Get Controller For Gamepad Index

Returns the associated controller handle for the specified emulated gamepad. Can be used with GetInputTypeForHandle to determine the controller type of a controller using Steam Input Gamepad Emulation.

```csharp
var handle = API.Input.Client.GetControllerForGamepadIndex(index);
```

### Get Current Action Set

Get the currently active action set for the specified controller.

```csharp
var handle = API.Input.Client.GetCurrentActionSet(controller);
```

### Get Digital Action Data

Returns the current state of the supplied digital game action.

```csharp
var data = API.Input.Client.GetDigitalActionData(controller, action);
```

### Get Digital Action Handle

Get the handle of the specified digital action.

{% hint style="warning" %}
This function does not take an action set handle parameter. That means that each action in your VDF file must have a unique string identifier. In other words, if you use an action called "up" in two different action sets, this function will only ever return one of them and the other will be ignored.
{% endhint %}

```csharp
var handle = API.Input.Client.GetDigitalActionHandle(actionName);
```

### Get Digital Action Origins

Use this to display the appropriate on-screen prompt for the action.

```csharp
var origins = API.Input.Client.GetDigitalActionOrigins(controller,
                                actionSet,
                                action);
```

### Get Gamepad Index for Controller

Returns the associated gamepad index for the specified controller, if emulating a gamepad.

```csharp
var index = API.Input.Client.GetGamepadIndexForController(controller);
```

### Get Glyph for Action Origin

Gets the local path to the art for an on-screen glyph of a particular origin

#### For PNG

```csharp
var imagePath = API.Input.Client.GetGlyphPNGForActionOrigin(origin, size, flags);
```

#### For SVG

```csharp
var imagePath = API.Input.Client.GetGlyphSVGForActionOrigin(origin, flags);
```

### Get Input Type for Controller handle

Returns the input type (device model) for the specified controller. This tells you if a given controller is a Steam controller, XBox 360 controller, PS4 controller, etc. For more details, see Steam's [Supported Controller Database](https://support.steampowered.com/kb\_article.php?ref=5199-TOKV-4426).

```csharp
var type = API.Input.Client.GetInputTypeForHandle(controller);
```

### Get Motion Data

Returns raw motion data for the specified controller.

```csharp
var data = API.Input.Client.GetMotionData(controller);
```

### Get String for Action Origin

Returns the localized string for the specified origin.

```csharp
var originName = API.Input.Client.GetStringForActionOrigin(origin);
```

### Initialize the Input System

This must be called before using API.Interface. It takes a single parameter `explicitlyCallRunFrame` which if true would require you to call `RunFrame()` to synchronize the state data.

```csharp
API.Input.Client.Init(explicitlyCallRunFrame);
```

### Run Frame

If you chose to initialize with explicitly run frame enabled you should call this before testing for input. In most cases you will initialize `API.Input.Client.Init(false);` and so this will be called for you each Update via the `Steamworks Behaviour`.

```
API.Input.Client.RunFrame();
```

### Set LED Color

Set the controller LED color on supported controllers.

{% hint style="info" %}
The VSC does not support any color but white, and will interpret the RGB values as a greyscale value affecting the brightness of the Steam button LED.&#x20;

The DS4 responds to full color information and uses the values to set the color & brightness of the lightbar.
{% endhint %}

```
API.Input.Client.SetLEDColor(controller, color);
```

### Reset LED Color

Resets the controllers LED color to the user's default.

```
API.Input.Client.ResetLEDColor(controller);
```

### Shutdown

This must be called when your done using the Input interface.

```
API.Input.Client.Shutdown();
```

### Show Binding Panel

Invokes the Steam overlay and brings up the binding screen.

```
API.Input.Client.ShowBindingPanel(controller);
```

### Stop Analog Action Momentum

Stops the momentum of an analog action (where applicable, ie a touchpad w/ virtual trackball settings).

{% hint style="info" %}
This will also stop all associated haptics. This is useful for situations where you want to indicate to the user that the limit of an action has been reached, such as spinning a carousel or scrolling a webpage.
{% endhint %}

```
API.Input.Client.StopAnalogActionMomentum(controller, action);
```

### Trigger Vibration

Trigger a vibration event on supported controllers.

{% hint style="info" %}
This API call will be ignored for incompatible controller models.&#x20;

This generates the traditional "rumble" vibration effect.&#x20;

The VSC will emulate traditional rumble using its haptics.
{% endhint %}

```
API.Input.Client.TriggerVibration(controller, leftSpeed, rightSpeed);
```

### Translate Action Origin

Get the equivalent origin for a given controller type or the closest controller type that existed in the SDK you built into your game if eDestinationInputType is k\_ESteamInputType\_Unknown. This action origin can be used in your glyph look up table or passed into GetGlyphForActionOrigin or GetStringForActionOrigin

```
API.Input.Client.TranslateActionOrigin(destination, source);
```

### Get Device Binding Revision

Gets the major and minor device binding revisions for Steam Input API configurations. Major revisions are to be used when changing the number of action sets or otherwise reworking configurations to the degree that older configurations are no longer usable. When a user's binding disagrees with the major revision of the current official configuration Steam will forcibly update the user to the new configuration. New configurations will need to be made for every controller when updating the major revision. Minor revisions are for small changes such as adding a new optional action or updating localization in the configuration. When updating the minor revision you generally can update a single configuration and check the "Use Action Block" to apply the action block changes to the other configurations.

```csharp
if(API.Input.Client.GetDeviceBindingRevision(controller, 
                                out int major,
                                out int minor))
{
     Debug.Log("v" + major + "." + minor);
}
else
{
     Debug.Log("Not found");
}
```

### Get Remote Play Session ID

Get the Steam Remote Play session ID associated with a device, or 0 if there is no session associated with it. See isteamremoteplay.h for more information on Steam Remote Play sessions.

```csharp
var id = API.Input.Client.GetRemotePlaySessionID(controller);
```
