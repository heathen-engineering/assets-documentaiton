# Input Action

## Definition

```csharp
public class InputAction : GameEvent<InputActionData>
```

Represents a Steam Input Action such as defined in your games [IGA ](../learning/core-concepts/steam-input.md#in-game-action-file)file.

These must be created as part of your [Steam Settings](steam-settings.md) object .

## Fields and Attributes

| Type                        | Name          | Comment                                                                                                              |
| --------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------- |
| InputActionType             | type          | The type of action (Analog or Digital)                                                                               |
| string                      | actionName    | The name of the action as it appears in the [IGA](../learning/core-concepts/steam-input.md#in-game-action-file) file |
| InputAnalogActionHandle\_t  | AnalogHandle  | The native Steam API handle if this is a analog handle and has been resolved.                                        |
| InputDigitalActionHandle\_t | DigitalHandle | The native Steam API handle if this is a digital handle and has been resolved.                                       |

## Methods

### Get Data

```csharp
public InputActionData this[InputHandle_t controller];
```

This returns the current cashed state for this action and for this controller, this does not update the state with the latest data from Steam it simply returns the last updated state. Typically you would have a behaviour poll all relivent actions at the start of an update and let various behaviours simply read the last known state for the actions they are interested in.

#### Example:

```csharp
public class PlayerController : MonoBehaviour
{
    Steamworks.InputHandle_t controller;
    public InputAction someAction;
    
    // ...
    
    private void Start()
    {
        controller = HeathenEngineering.SteamworksIntegration.API.Input.Client.ConnectedControllers[0];
    }
    
    //...
    
    private void Update()
    {
        SteamSettings.Client.UpdateAllActions(controller);
        
        var actionData = someAction[controller];
        if(actionData.active)
            Debug.Log("Engaged: " + actionData.state);
    }
}
```

Once you have a script updating the status of your actions other behaviours can simply read that most recent state;

```csharp
public class SomeOtherBehaviour : MonoBehaviour
{
    Steamworks.InputHandle_t controller;
    public InputAction otherAction;
    
    // ...
    
    private void Start()
    {
        controller = HeathenEngineering.SteamworksIntegration.API.Input.Client.ConnectedControllers[0];
    }
    
    // ...
    
    private void Update()
    {
        var actionData = otherAction[controller];
        if(actionData.active)
            Debug.Log("Engaged: " + actionData.state);
    }
}
```

### Update Status

```csharp
public void UpdateStatus(InputHandle_t controller);
```

Call this to update the state of the action for the indicated controller.

#### Example:

```csharp
var controller = Input.Client.ConnectedControllers[0];
// ...
testAction.UpdateStatus(controller);
```

You can optionally call this for all actions at once via the Steam Settings object

```csharp
var controller = Input.Client.ConnectedControllers[0];
// ...
SteamSettings.Client.UpdateAllActions(controller);
```

### Get Input Glyphs

```csharp
public Texture2D[] GetInputGlyphs(InputHandle_t controller, InputActionSet set);
```

```csharp
public Texture2D[] GetInputGlyphs(InputHandle_t controller, InputActionSetLayer set);
```

```csharp
public Texture2D[] GetInputGlyphs(InputHandle_t controller, InputactionSetHandle_t set);
```

This returns the set of textures related to the action for the given controller and action set. For example if this action exists on the indicated set and is mapped to the B button and Right Trigger then the B button texture and RT texture will be returned.&#x20;

The images for these can be configured in your app.

#### Examples:

```csharp
var images = action.GetInputGlyphs(controller, actionSet);
// ...
rawImage.Texture = images[0];
```

### Get Input Names

```csharp
public string[] GetInputNames(InputHandle_t controller, InputActionSet set);
```

```csharp
public string[] GetInputNames(InputHandle_t controller, InputActionSetLayer set);
```

```csharp
public string[] GetInputNames(InputHandle_t controller, InputactionSetHandle_t set);
```

This returns the set of names related to the action for the given controller and action set. For example if this action exists on the indicated set and is mapped to B and Right Trigger then the string "B Button" and "Right Trigger" will be returned.

#### Examples:

```csharp
var names = action.GetInputNames(controller, actionSet);
// ...
label.Text = names[0];
```

## How To

### Create

Input Actions are created as part of your [Steam Settings](steam-settings.md) object

![](<../../../.gitbook/assets/image (160) (1).png>)

### Set Analog or Digital

Click the AI or DI buttton to change the type

AI represents "Analog Input"

DI represents "Digital Input"

![](<../../../.gitbook/assets/image (161) (1) (1).png>)
