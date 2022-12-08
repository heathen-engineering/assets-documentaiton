---
description: Reading input actions in game
---

# Reading Input

<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

How to read input from Steam Input using Heathen's Steamworks Complete. This article assumes you have already set up input actions in your Steam Portal for your app.&#x20;

{% hint style="info" %}
You must have completed [this step](https://partner.steamgames.com/doc/features/steam\_controller/getting\_started\_for\_devs#publishing)!\
That is you must have set up the default actions for your app in your portal and published those changes.
{% endhint %}

{% embed url="https://partner.steamgames.com/doc/features/steam_controller/getting_started_for_devs#publishing" %}
Step 4: Publishing
{% endembed %}

Assuming you have a working set of input actions defined for your app and you can configured them in your Steam Settings, see the [Setup article](getting-started.md) for more information.

## [Steam Input Manager](../../components/steam-input-manager.md)

Before you can use Steam Input you need to enable it. We have created a tool for you that will handle this ... see Steam Input Manager for details. Alternatively you can do this your self with just a few lines of code if you prefer.

### Creating your own

Input Manager really only does 3 things for you

1. Initialize and Dispose the Input system\
   To do this you need to call [API.Input.Client.RunFrame](../../../api/input.md#run-frame) on start. In UnityEditor you should also call `Application.OpenURL($"steam://forceinputappid/{SteamSettings.ApplicationId}");` to force Steam client to use your app's input settings\
   And when your done call `Application.OpenURL("steam://forceinputappid/0");`
2. Get the list of controllers e.g.\
   `controllers = API.Input.Client.ConnectedControllers;` you'll need these for step 3
3. Update all actions for all controllers e.g.\
   foreach over each conntorller and call: `SteamSettings.Client.UpdateAllActions(controller);` on it.

For a functional codded example simply review the source code of SteamInputManager.cs

## Direct Read

When you simply want to check the value of an input action. Lets assume you have created a reference to your desired InputAction in your class object such as.

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

This of course assumes you want to read data from the first controller and that you have made sure there is a controller. What this returns is an [InputActionData](../../../objects/input-action-data.md) object which can be used to understand the current state of the action.

## [Input Action Events](../../components/input-action-event.md)

We created [InputAction ](../../scriptable-objects/input-action.md)as a type of [Game Event](../../../../system-core/game-events.md). So this means you can register to and listen for changes on each input action from any where. We have tools like the [Input Action Event](../../components/input-action-event.md) that let you set this up easily in Unity Editor's Inspector.

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
