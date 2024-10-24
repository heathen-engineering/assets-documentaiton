---
description: Advanced logging features made easy
---

# LogData

## Introduction

The LogData object is used by the Log API to store system and event information and facilitate the use of that information.

## Definition

### Fields and Attributes

<table><thead><tr><th width="226.53266678954236">Type</th><th width="193.13335237910752">Name</th><th width="297.85630306988895">Comment</th></tr></thead><tbody><tr><td>string</td><td>companyName</td><td>The name of the company as defined in the project settings.</td></tr><tr><td>string</td><td>productName</td><td>The name of the app as definned in thee project settings.</td></tr><tr><td>string</td><td>engineVersion</td><td>The version of the Unity engine this build was made with</td></tr><tr><td>string</td><td>commandLine</td><td>The command line used to launch this instance</td></tr><tr><td>string</td><td>platform</td><td>The platform the instance is running on as reported by the Unity Engine</td></tr><tr><td>string</td><td>deviceType</td><td>The type of device the instance is running on as reported by the Unity Engine.</td></tr><tr><td>string</td><td>deviceName</td><td>The name of the device as reported by the hardware</td></tr><tr><td>string</td><td>os</td><td>The operating system name as reported by the Unity Engine.</td></tr><tr><td>string</td><td>osFamily</td><td>The operating system gamily as reported by the Unity Engine.</td></tr><tr><td>string</td><td>cpuType</td><td>The CPU type as reported by the Unity Engine.</td></tr><tr><td>int</td><td>cpuCount</td><td>The number of CPUs available as reported by Unity Engine.</td></tr><tr><td>int</td><td>cpuFrequency</td><td>The CPU clock frequency as reported by the Unity Engine.</td></tr><tr><td>int</td><td>systemMemory</td><td>The amount of system memory available as reported by Unity Engine.</td></tr><tr><td>string</td><td>gpuVendor</td><td>The vendor name of the detected GPU as reported through Unity Engine</td></tr><tr><td>string</td><td>gpuType</td><td>The GPU type as reported by the Unity Engine.</td></tr><tr><td>string </td><td>gpuName</td><td>The name of the GPU as reported by Unity Engine.</td></tr><tr><td>string </td><td>gpuVersion</td><td>The version string of the GPU as reported by Unity Engine.</td></tr><tr><td>int</td><td>gpuMemory</td><td>The available GPU memory as reported by Unity Engine.</td></tr><tr><td>int</td><td>gpuShaderLevel</td><td>The supported shader level as reported by Unity Engine.</td></tr><tr><td>List&#x3C;Entries></td><td>entries</td><td>The recorded log entries for this session.</td></tr></tbody></table>

### Methods

```csharp
public void Add(string message, string stack, LogType type);
```

Adds a new entry to the entries collection

```csharp
public override string ToString();
```

Outputs a human friendly text version of the log

```csharp
public string ToJson();
```

Outputs a JSON formated string version of the log

```csharp
public string SaveJson(string fileName, string path=null);
```

Saves the JSON output of the log to a location on disk. If the path is not provided the persistentDataPath as defined by Unity Engine will be used. The return value is the full path of the file that was writen.

```csharp
public string SaveText(string fileName, string path=null);
```

Saves the Text output of the log to a location on disk. If the path is not provided the persistentDataPath as defined by Unity Engine will be used. The return value is the full path of the file that was writen.
