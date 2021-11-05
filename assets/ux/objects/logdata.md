---
description: Advanced logging features made easy
---

# LogData

## Introduction

The LogData object is used by the Log API to store system and event information and facilitate the use of that information.

## Definition

### Fields and Attributes

| Type           | Name           | Comment                                                                        |
| -------------- | -------------- | ------------------------------------------------------------------------------ |
| string         | companyName    | The name of the company as defined in the project settings.                    |
| string         | productName    | The name of the app as definned in thee project settings.                      |
| string         | engineVersion  | The version of the Unity engine this build was made with                       |
| string         | commandLine    | The command line used to launch this instance                                  |
| string         | platform       | The platform the instance is running on as reported by the Unity Engine        |
| string         | deviceType     | The type of device the instance is running on as reported by the Unity Engine. |
| string         | deviceName     | The name of the device as reported by the hardware                             |
| string         | os             | The operating system name as reported by the Unity Engine.                     |
| string         | osFamily       | The operating system gamily as reported by the Unity Engine.                   |
| string         | cpuType        | The CPU type as reported by the Unity Engine.                                  |
| int            | cpuCount       | The number of CPUs available as reported by Unity Engine.                      |
| int            | cpuFrequency   | The CPU clock frequency as reported by the Unity Engine.                       |
| int            | systemMemory   | The amount of system memory available as reported by Unity Engine.             |
| string         | gpuVendor      | The vendor name of the detected GPU as reported through Unity Engine           |
| string         | gpuType        | The GPU type as reported by the Unity Engine.                                  |
| string         | gpuName        | The name of the GPU as reported by Unity Engine.                               |
| string         | gpuVersion     | The version string of the GPU as reported by Unity Engine.                     |
| int            | gpuMemory      | The available GPU memory as reported by Unity Engine.                          |
| int            | gpuShaderLevel | The supported shader level as reported by Unity Engine.                        |
| List\<Entries> | entries        | The recorded log entries for this session.                                     |

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
