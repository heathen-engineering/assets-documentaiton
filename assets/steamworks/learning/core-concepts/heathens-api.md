---
description: Getting started with the Heathen Steam API
---

# Heathen's API

Heathen's Steam API is a wrapper around Steamworks.NET whcih is its self a wrapper around Valve's own Steam API.

Valve's Steam API is written in C/C++ has questionable documentaiton :wink: and uses programming styles forigne to most Unity developers and even most C# programmers.

Steamworks.NET is a true to form wrapper around Valve's Steam API. This means that while the syntax has been updated to use C# styling the design paradigm is still very much a relic of older and more importantly unmanaged styles. One of the most obvsious examples of this is the use of Callback and CallResult to handle deligates.

Heathen's API wraps around Steamworks.NET adjusting the design of the interfaces to conform not only to common C# standards but more importantly to Unity's common standards. We have wrapped every Callback with a UnityEvent, we have wrapped every CallResult with an Action, we simplify enumeration to yield .NET collections (typically arrays for sake of performance) and we have wrapped abstract data types such as CSteamID with helpers such as UserData, Clan, etc. to reduce ambiguity and reduce the required steps to access information or perform common operations.

## Callbacks

On any feature of the Steam API wher a SteamCallback handle would have been used aka a CallResult, you will find that we have added an Action\<T,bool> callback paramiter.

```csharp
public static void ExampleMethod(int inputData, Action<OutputType, bool> callback)
```

notice the signature of the action, the typical form with all Steam API call result deligates is that the first paramiter is what ever the resulting requests data type is and the second is a boolean. The boolean represents an IO Failure and is pesamistic, consider the following example handler.

### Using Expression

```csharp
ExampleMethod(42, (result, bIOError) =>
{
    if(bIOError)
        Debug.Log("An IO error occured, responce data is unreliable");
    else
        Debug.Log("No IO error, check the result for more info")
});
```

### Classic

```csharp
ExampleMethod(42, HandleExampleResult);

//...

private void HandleExampleResult(int result, bool bIOError)
{
    if(bIOError)
        Debug.Log("An IO error occured, responce data is unreliable");
    else
        Debug.Log("No IO error, check the result for more info")
}
```

## Static Classes

Like the native Steam API all of the "interfaces" are static classes and are wrapped up in the API namespace. To insure you do not have any ambigious calls in your code we recomend that you use the follow Heathen namespace.

```csharp
using HeathenEngineering.SteamworksIntegration;
```

And then in your code where you would like to access one of our interfaces you can use its namespace and interface name.

```csharp
var localUser = API.User.Client.Id;
```

or

```csharp
var clans = API.Clans.Client.GetClans();
```

and similar, the following articles will explain in detail each of the available interfaces and provide examples for use. You can also find samples in the asset package you install from the Unity Package Manager.
