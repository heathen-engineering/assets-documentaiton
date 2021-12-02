# 6 Input



{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of Steam Input API

![](<../../../../.gitbook/assets/image (176).png>)

### What do I learn?

1. Using steam's [Input](../../api/input.md) API
2. How to access the Knowledge Base (where you are now)
3. How to acces the support [Discord ](https://discord.gg/6X3xrRc)
4. How to leave a review 😉

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



The sample scene should clear this when it exits however if you find your Steam Input findings are stuck on App 480 (Spacewars) you can run the command

[steam://forceinputappid/0](steam://forceinputappid/0) to force it to clear&#x20;
{% endhint %}

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### DEMO SCRIPTS

The demo script for this scene operates the Steam Input API. The following instructions discribe what it does and why

## Use

### Initalize

Before you can use Steam Input at all you must initalize it. While Valve states that the RunFrame operation will happen automatically with the general API update we have found that its best to explicitly call the Run Frame command and to initalize it accordingly.

```csharp
SteamworksIntegration.API.Input.Client.Init(true);
```

You can learn more about this funciton in the [Input API](../../api/input.md#initalize-the-input-system) article.

{% hint style="info" %}
The sample scene does this in the Start method the Sample6Behaviour script.
{% endhint %}

### Controllers

Next you will want to fetch the set of controllers available to the Steam Input system. you can do this simply by reading the ConnectedControllers field. Note we want to cashe this so we aren't having to iterate over all controllers every time we want to get one.

```csharp
controllers = SteamworksIntegreation.API.Input.Client.ConnectedControllers;
```

{% hint style="info" %}
The sample scene does this in the Start method of the Sample6Behaviour script.
{% endhint %}

By cashe we mean that we store this in a varaible on our script so we dont need to call it each time we want to use it.

### Loading Handles

The Steam Input system works by identifying control sets and control actions via "handles" these are simply numbers that represent that specific control set or control action and are quicker than parsing strings each time.

So we want to cashe the handles for all of the sets and actions we will be using once and use the handles as required.

```csharp
shipControlHandle = SteamworksIntegration.API.Input.Client.GetActionSetHandle(shipControlSet);

analogActionHandle = SteamworksIntegration.API.Input.Client.GetAnalogActionHandle(analogAction);

leftActionHandle = SteamworksIntegration.API.Input.Client.GetDigitalActionHandle(turnLeft);
```

In the above example taken from the Sample6Behaviour script the `shipControlSet` is a string being the name of the control set, `analogAction` is a string being the name of an analog control action and `turnLeft` is a string being the name of a digital control action.

We store the resulting handles in variables local to our script for quicker access later.

{% hint style="info" %}
The sample scene does this in the Start method of the Sample6Behaviour script.
{% endhint %}

### Activating Action Sets

Now that we have the handles for our sets and actions we need to tell Steam Input API which set of actions we would like to listen for. To do this we will call ActivateActionSet on the desired action set.&#x20;

```csharp
SteamworksIntegration.API.Input.Client.ActivateActionSet(controllers[0], menuControlHandle);
```

Note that we need to identify whcih controller we are activating this action set for. in this example we are simply assuming the first controller found is the main one. This call has a low overhead according to Steam and can be called repeatedly so for sake of ease in our demo we call this every frame based on what we calcualte should be active.

In the case of our sample scene we activate the menu when a toggle is true and the ship controls when it is false.

{% hint style="info" %}
The saple scene does this in the Update method of the Sample6Behaviour script.
{% endhint %}

### Getting Input Data

Now that we have an active action set we need to know what actions are active and what the input values are for them.

Digital Action Data is the simplest form and typical of a computer style button that is a value of on or off with no inbetween.

```csharp
var data = SteamworksIntegration.API.Input.Client.GetDigitalActionData(controllers[0], leftActionHandle);
```

So to do this we pass in the controller we want to test and what action we want to test for. Notice that we do not specify what action set. You cannot have overlaping actions in mutliple sets if you do the input API will operate on 1 and ignore the other.

The result data will be of type `Steamworks.InputDigitalActionData_t` and will contain 2 fields of relivence.

```csharp
byte bActive;
byte bState;
```

Steam uses byte in place of bool in most cases, a value of 0 here indicates false and 1 indicates true.

bActive indicates that the action is active and being monitored by the interface

bState is what the last known state was e.g. false for not pressed and true for pressed

Analog data is similar

```csharp
var data = SteamworksIntegration.API.Input.Client.GetAnalogActionData(controllers[0], analogActionHandle);
```

data in this case will have 4 values of relivence

```csharp
EInputSourceMode eMode;
float x;
float y;
byte bActive;
```

The eMode indicates what kind of analog input this is e.g. Dpad, Buttons, Joystick, etc.

The x and y values indicate a range from 0 to 1 for no input to max input

bActive as it does with digital input indicates rather or not this action is beign monitored.

{% hint style="info" %}
In our sample scene we have created serializable mimics of the analog and digital data objects so that we can display them easily in the inspector. You do not need to do this, just use the Steam versions directly.



You can see where we read each action in the Update method of the Sample6Behaviour script.
{% endhint %}
