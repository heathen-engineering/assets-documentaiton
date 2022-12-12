---
description: Working with Steam's BigPicture Mode
---

# BigPicture.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

```csharp
using BigPicture = HeathenEngineering.SteamworksIntegration.API.BigPicture.Client;
```

```csharp
public static class BigPicture.Client
```

This leverages features of ISteamUtil to simplify working in Steam's BigPicture mode. In particular tests for "IsBigPicutre", "RunningOnStemDeck" and handling Gamepad Text Input.

## Events

### EventGamepadTextInputShown

This is invoked when the Gamepad Text Input feature of Steam's Big Picture mode is displayed to the user. This only occurs when your game triggers it by calling [ShowTextInput](bigpicture.client.md#undefined).

```csharp
public static UnityEvent EventGamepadTextInputShow => get;
```

This event has no arguments so its handler is simply

```csharp
void HandleGamepadTextInputShownEvent()
{
    // Do work when the Gamepad Text Input is shown
}
```

### EventGamepadTextInputDismissed

This is invoked when the Gamepad Text Input feature of Steam's Big Picture mode is dismissed e.g. closed and carries the resulting text it captured.

```csharp
public static UnityStringEvent EventGamepadTextInputDismissed => get;
```

This event has 1 argument of type string so its handle should take the form of

```csharp
void HandleGamepadTextInputDismissed(string result)
{
    // Result is the string the user typed with the gamepad
}
```

## Fields and Attributes

### InBigPicture

```csharp
public static bool InBigPicture => get;
```

Returns true if the Steam client is running in Big Picture mode.

### RunningOnDeck

```csharp
public static bool RunningOnDeck => get;
```

Returns true if the app is running on a Steam Deck

## Methods

### ShowTextInput

Activates the big picture text input dialog which only supports gamepad input.

{% hint style="warning" %}
This is not a virtual keyboard, it is dependent on the Steam client being in Big Picture mode and cannot be used when it is not.

\
Steam does have a virtual keyboard that you can use. Please see the Utilities API for more information.
{% endhint %}

```csharp
public static bool ShowTextInput(
                EGamepadTextInputMode inputMode,
                EGamepadTextInputLineMode lineMode,
                string description, 
                uint maxLength, 
                string currentText)
```

Returns true if the client is in Big Picture mode false otherwise

#### inputMode

Selects the input mode to use, either Normal or Password (hidden text)

#### lineMode

Controls whether to use single or multi line input.

#### description

Sets the description that should inform the user what the input dialog is for.

#### maxLength

The maximum number of characters that the user can input.

#### currentText

Sets the pre-existing text which the user can edit.
