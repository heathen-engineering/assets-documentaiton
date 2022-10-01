---
description: Features from ISteamUtil with a few extras from Heathen!
---

# Utilities.Client

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using SteamUtils = HeathenEngineering.SteamworksIntegration.API.Utilities.Client;
```

```csharp
public static class Utilities.Client
```

This leverages features of ISteamUtil to simplify working for Steam's Virtual Keyboard and launcher features..

## Events

### EventAppResumFromSuspend

Invoked when the app regains focus from suspend as seen by Steam Client.

```csharp
public static UnityEvent EventAppResumFromSuspend => get;
```

This event has no arguments so its handler will take the form of

```csharp
void HandleAppResumFromSuspendEvent()
{
    // The app has just resumed
}
```

### EventKeyboardShown

Invoked when the Steam virtual keyboard is shown to the user. This virtual keyboard sends OS Key events so should trigger Unity's input systems normally. It is only shown to the user when you request it via the [ShowVirtualKeyboard ](utilities.client.md#undefined)method.

```csharp
public static UnityEvent EventKeyboardShown => get;
```

This event has no arguments

{% hint style="success" %}
But how do I get the text?

It is a true virtual keyboard, so Unity's Input system should be triggered by the key strokes as if it was a real keyboard.
{% endhint %}

```csharp
void HandleKeyboardShownEvent()
{
    // The virtual keyboard has been shown
}
```

### EventKeyboardClosed

Invoked when the Steam virtual keyboard is closed.

```csharp
public static UnityEvent EventKeyboardClosed => get;
```

This event has no arguments

{% hint style="success" %}
But how do I get the text?

It is a true virtual keyboard, so Unity's Input system should be triggered by the key strokes as if it was a real keyboard.
{% endhint %}

```csharp
void HandleKeyboardClosedEvent()
{
    // The virtual keyboard has been closed
}
```

## Fields and Attributes

### IP Country

```csharp
public static string IpCountry => get;
```

### Seconds Since App Active

```csharp
public static uint SecondsSinceAppActive => get;
```

### Server Real Time

```csharp
public static DateTime ServerRealTime => get;
```

### Steam UI Language

```csharp
public static string SteamUILanguage => get;
```

### Big Picture Mode

```csharp
public static bool IsSteamInBigPictureMode => get;
```

### In VR Mode

```csharp
public static bool IsSteamRunningInVR => get;
```

### In Steam Deck

```csharp
public static bool IsSteamRunningONSteamDeck => get;
```

### VR Streaming Enabled

```csharp
public static bool IsVRHeadsetStreamingenabled => get;
```

## Methods

### SetGameLauncherMode

In game launchers that don't have controller support you can call this to have Steam Input translate the controller input into mouse/kb to navigate the launcher

```csharp
public static void SetGameLauncherMode(bool mode);
```

#### mode

Whether a launcher is active or not

### StartVRDashboard

Asks Steam to create and render the OpenVR dashboard.

```csharp
public static void StartVRDashboard();
```

### ShowVirtualKeyboard

Opens a floating keyboard over the game content and sends OS keyboard keys directly to the game. The text field position is specified in pixels relative the origin of the game window and is used to position the floating keyboard in a way that doesn't cover the text field.

{% hint style="success" %}
But how do I get the text?

It is a true virtual keyboard, so Unity's Input system should be triggered by the key strokes as if it was a real keyboard.
{% endhint %}

```csharp
public static bool ShowVirtualKeyboard(
                EFloatingGamepadTextInputMode mode, 
                int2 fieldPosition, 
                int2 fieldSize)
```

returns **true** if the floating keyboard was shown, otherwise, **false**.

#### mode

Selects the keyboard type to use

#### fieldPosition

Coordinate of where to position the floating keyboard

#### fieldSize

Desired size of the floating keyboard
