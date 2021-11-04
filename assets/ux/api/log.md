---
description: Better recording for all your log needs
---

# Log

## Introduction

```csharp
public static class API.Log
```

The log interface provides and enhanced system log and can be used on its own or in conjunction with user reporting and feedback systems.

### What can it do?

Heathen's log does everything Unity's built in log does, including recording Debug.Log messages and exceptions but it also gathers system data about the running application and the machine executing it and provides helpful tools for for storing and sending that log inforamtion so you can make better use of it.

## How To

### Enable the log system

The log system must be enabled if you intend to use it. This will cause the system to register to the applications message thread and start recording relivent information. You can enable and disable the log at will.

```csharp
API.Log.Enabled = true;
```

### Date Formating

The log system records detailed time for each event and can express this time in any format you would like. The default formate will provide full date time including time zone information.

```csharp
API.Log.dateTimeFormat = "yyyy-MM-dd HH:mm:ss zzzz";
```

### Enable Stack Tracing

You can optionally output stack trace information with your log. Note that this is limited to the information available to the .NET Exception object or Unity message that inizted the log event.

This is disabled by default.

```csharp
API.Log.logStackTrace = true;
```

### Output the log

You can output the log in 4 different forms each appropreate for a different use.&#x20;

For human consumption you should use the Text form. In this for the system will format the log as a human friendly text file.

```csharp
var text = API.Log.Text;
```

You can output as a JSON string as well ... this is useful for programitic reading of the log

```csharp
var jsonString = API.Log.Json;
```

finally you can output the log as binary data suitable for transmission over a network, storage to a file or attachment to reporting systems such as Unity's User Reporting service.

```csharp
var data = API.Log.Bytes;
```

Alternativly you could take the log object and output it however you like.

```csharp
LogData logObj = API.Log.Object;
```

### Reading a log

You can use this API to read complex logs as well. The LogData object defines the structure of the log and the interface can parse JSON and byte\[] data into a LogData object.

```csharp
var logObj = API.Log.Parse(jsonString);
```

or

```csharp
var logObj = API.Log.Parse(byteData);
```

### Resetting a log

While rare there are occasions where you might want to clear the log of all its current entries. You can use the following command.

```csharp
API.Log.Reset();
```

### Save to file

You can save a log to file as either human friendly text or as a JSON file

```csharp
API.Log.SaveToTextFile(name, path);
```

or

```csharp
API.Log.SaveToJsonFile(name, path);
```

### Record a log entry

The Heathen log system connects to Unity's internal log and so in most cases you can just keep using your typical Debug.Log statements. There are some cases though where you may prefer to log a manual message type and so you can use.

```csharp
API.Log.LogManual(message, stack, type);
```

### Attaching to Trello

You can use the Log along side the Trello API to upload the log as an attachment. See the Terllo article for details.

### Attaching to Unity User Reporting

Unity User reporting can take attachments as byte\[] data. To do attach a log then you would simply specify the attachment document type as "application/json" and provide it with the binary output of the log e.g. `API.Log.Bytes`

### Attaching to Email

This will depend on the platform in question. How exsactly you attach or relate the log to that platforms email system is up to you. As to getting the data you can use the Save to file features to create a local save and attach that or you can use the Bytes output to attach the file as a byte\[] similar to what would be done with Unity's User Reporting.
