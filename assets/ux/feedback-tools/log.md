---
description: User eXperience's custom log tool
---

# Log

## Introduction

The custom log tool provided with User eXperience works similar to Unity's built in log. In fact you do not need to do anything special to use it other than enable it in your Feedback Configuration. Unity's Debug.Log commands will still write to the custom log just like it does to Unity's built in log.

The main advantage to User eXperience's custom log is the inclusion of much more rich user data and the ability to strip stack trace data making for a more compact log. The custom log is also capable of printing time stamps with UTC offset for situations where you need to reliably link messages to a point in time, such as to coralate between a client log and server log.

The custom log has 1 more important feature, while it can be saved as a text file or parsed out as a human friendly string to a web service or similar its also possible to export the log as JSON making it much easier to work with in backend services or with custom web services.

## System Information

The custom log as noted gathers additional rich information about the target system and makes it available in the text and JSON exports. The following data is available in addition to the list of events detected at run time.

### Company Name

The name provided in your Project's Player Settings

### Product Name

The name provided in your Project's Player Settings

### Product Version

The version provided in your Project's Player Settings

### Engine Version

The version of Unity the game was built on

### Command Line Arguments

The command line arguments passed in when the game was launched

### Platform

The platform (as defined by Unity) the game is running on

### Device Type

The type of device the game is running on e.g. mobile, desktop, etc.

### Device Name

Typically the network name of the device the game is running on

### Operating System

The name of the operating system as reported by System Information

### Operating System Family

The type of operating system as reported by System Information e.g. Mac, Linux, Windows, Other

### CPU Type

The hardware reported CPU type

### CPU Count

The number of cores reported to the hardware system

### CPU Frequency

The frequency of the CPU as reported to the hardware system

### System Memory

The amount of system memory visible to the hardware system

### GPU Vendor

The vendor associated with the GPU e.g. "ATI Technologies Inc."

### GPU Type

The API type used by the GPU such as Direct3D12, Vulkan, etc.&#x20;

{% embed url="https://docs.unity3d.com/ScriptReference/Rendering.GraphicsDeviceType.html" %}

### GPU Name

The name of the graphics card as reported by the graphics driver

### GPU Version

A string reported by the graphics driver expressing the low level graphics API kind and driver version such as "Direct3D 0.0c \[atiumdag.dll 7.14.10.471]"

### GPU Memory

The amount of memory available to the graphics device

### GPU Shader Level

An integer representing the shader level supported by the graphics device

{% embed url="https://docs.unity3d.com/ScriptReference/SystemInfo-graphicsShaderLevel.html" %}

## Examples

### Get Log

This can be used to fetch the log in memory such as to send over the network or print in game.

#### To String

```csharp
FeedbackSystem.Log.ToString();
```

#### To Json

```csharp
FeedbackSystem.Log.ToJson();
```

### Save Log

{% hint style="info" %}
Path is an optional parameter that if left null or omitted the system will save the log to the persistent data path, as defined by the Unity Engine. Where exactly this is depends on the platform.
{% endhint %}

{% hint style="warning" %}
In all cases the call to Save the log will always return the path that the log was written to.
{% endhint %}

#### To Text

This will save the log to a human friendly text file similar to the standard Unity log file.

```csharp
FeedbackSystem.Log.SaveText(fileName, path);
```

#### To JSON

This will save the log to a JSON formatted string stored in a file.

```csharp
FeedbackSystem.Log.SaveJson(fileName, path);
```
