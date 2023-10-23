---
cover: ../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Unity Input

### [Action Set](../../heathens-steamworks-complete/unity/scriptable-objects/input-action-set.md)

An action set is simply a container of layers and actions. For example, you might have 1 set of actions you use in your menu and another you use in gameplay so you might have an action set `menuActions` and another `gameActions` .

### [Action Set Layer](../../heathens-steamworks-complete/unity/scriptable-objects/input-action-set-layer.md)

An action set layer is a mask laid over the top of an action set. They are defined as a member of the action set and simply modify the set of actions activated by the set. An example might be a layer that adds extra mappings such as a sniper mode when a valid weapon is equipped or vehicle-type specific actions such as gas, brake, throttle up/down, etc.

### [Action](../../heathens-steamworks-complete/unity/scriptable-objects/input-action.md)

An action is ... well the action the player has requested such as jump, walk, shoot, etc. These are defined as members of an action set or action set layer and can specify what kind of action they are e.g. analogue or digital and if analogue what mode e.g. stick, absolute mouse, etc.

## Use

Once you have created your In-Game Action file; For more information on that read here [https://partner.steamgames.com/doc/features/steam\_controller/iga\_file](https://partner.steamgames.com/doc/features/steam\_controller/iga\_file)

Steam Input actions, sets and layers can be referenced in your [Steam Settings](../../heathens-steamworks-complete/unity/scriptable-objects/steam-settings/) object. Simply expand the Artifacts section and add each action, layer and set, this will create Scriptable Object representations for each under your Steam Settings object in your Asset folder. You can then reference these objects in your other scripts to detect when the action has been triggered and with what values.

![](<../../.gitbook/assets/image (158) (1) (1) (1).png>)

### Analog vs Digital Actions

You can toggle your Action types by simply clicking the AI/DI button

AI represents an "Analog Input"

DI represents a "Digital Input"

## Reading Input

### [Steam Input Manager](../../heathens-steamworks-complete/unity/components/steam-input-manager.md)

Before you can use Steam Input you need to enable it. We have created a tool for you that will handle this ... see Steam Input Manager for details. Alternatively, you can do this yourself with just a few lines of code if you prefer.

### Creating your own input manager

Input Manager only does 3 things for you

1. Initialize and Dispose of the Input system\
   To do this you need to call [API.Input.Client.RunFrame](../../heathens-steamworks-complete/unity/api/input.client.md#run-frame) on start. In UnityEditor you should also call `Application.OpenURL($"steam://forceinputappid/{SteamSettings.ApplicationId}");` to force Steam client to use your app's input settings\
   And when your done call `Application.OpenURL("steam://forceinputappid/0");`
2. Get the list of controllers e.g.\
   `controllers = API.Input.Client.ConnectedControllers;` you'll need these for step 3
3. Update all actions for all controllers e.g.\
   foreach over each controller and call: `SteamSettings.Client.UpdateAllActions(controller);` on it.

For a functional codded example simply review the source code of SteamInputManager.cs

## Direct Input Read

When you simply want to check the value of an input action. Let's assume you have created a reference to your desired InputAction in your class object such as.

```csharp
public class ExampleClass : MonoBehaviour
{
    public InputAction myAction;
}
```

Then you can read the state of that action for a given controller&#x20;

```csharp
var inputData = myAction[SteamInputManager.Controllers[0]];
```

This of course assumes you want to read data from the first controller and that you have made sure there is a controller. What this returns is an [InputActionData](../../heathens-steamworks-complete/unity/objects/input-action-data.md) object which can be used to understand the current state of the action.

## [Input Action Events](../../heathens-steamworks-complete/unity/components/input-action-event.md)

We created [InputAction ](../../heathens-steamworks-complete/unity/scriptable-objects/input-action.md)as a type of [Game Event](../../assets/system-core/game-events.md). So this means you can register to and listen for changes on each input action from any where. We have tools like the [Input Action Event](../../heathens-steamworks-complete/unity/components/input-action-event.md) that let you set this up easily in Unity Editor's Inspector.

You can also register for events in script just as easily

```csharp
myAction.AddListener(HandleActionEvent);
```

This would assume that HandleActionEvent looked like this

```csharp
private void HandleActionEvent(EventData<InputActionUpdate> data)
{
    //Do Work
    if(data.value.State)
        ;//This action happened
}
```
