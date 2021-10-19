---
description: Get player feedback with rich game data to help improve your game.
---

# Player Feedback System

## Introduction

The Feedback System included with the User eXperience kit helps you gather rich game data in a well formatted log, and then to feed that data from within your game to email or 3rd party tools such as Trello, Zendesk, etc. and to help you capture and save screenshots for the full screen or sections of the screen.

![](<../../../.gitbook/assets/image (92).png>)

## Features

### Custom Log

A custom log system which stores all Debug.Log messages with optional stack trace information, and additional system information is generated at run time. The log can be reported as a simple text log or serialized to a JSON object for easier pragmatic processing.

### Email Submit

The system stores a target email address and can prepare a mailto link opening the system default email tool.

### Trello Integration

The system stores API information for a given Trello account and can submit reports, logs and screen shots to target Trello lists. The Trello integration includes facilities to list cards, lists and boards related to the Trello account.

### Easy 3rd Party Extension

The system is designed to be easily integrated with the reporting tools of your choice. The log produced can be exported as simple text or as a JSON object for easy parsing by other tools, and includes an easy to use Screenshot tool capable of capturing a full screen or any defined rect of a screen, and returning that data as a Texture2D or quickly saving it out as a Jpg or Png.

## Configuration

![](<../../../.gitbook/assets/image (93).png>)

The Feedback System requires a Feedback Configuration object. The intent is that you as a developer will create your own custom Feedback Configuration object derived from the Feedback Configuration base class. The purpose of the configuration is to expose on demand the Email Address, Trello API Key, Terllo List ID and Trello Token for use with the feedback system's reporting functions.

{% hint style="info" %}
A `SimpleFeedbackConfiguration` class is provided with the asset, and will be sufficient for most projects. The Feedback Configuration base class simply allows you the developer to create your own configuration, such as to read configuration data from a web source, to obscure configuration, etc.
{% endhint %}

![Screenshot of the Simple Feedback Configuraiton inspector](<../../../.gitbook/assets/image (94).png>)

### Enable Custom Log

When set to true the User eXperience log will be used. This log is far more robust than Unity's standard log, and is capable of outputting simple text or JSON data as required.

{% hint style="info" %}
The custom log will contain all the data that the standard Unity log does, in addition it will also contain system information
{% endhint %}

You can read more about the User eXperience log in its [Knowledge Base article](log.md)

### Log Stack Trace

When set the log will also contain the stack trace information feed in by the messaging system.

### Log Date Time Format

The string format of time stamps in the log.&#x20;

{% hint style="info" %}
Its strongly advised to add the `z` or `zz` or `zzz` or `zzzz` at the end of your time format. the lower case z indicates that the UTC offset should be printed and this indicates the time zone. For example\
\
yyyy-MM-dd HH:mm:ss zzzz\
\
Should print a time such as\
2020-07-12 14:09:16 +01:00

The above indicates that the provided time is UTC+1 or 1 hour forward of the Universal Time Code.
{% endhint %}

### Email

The email address to prepare mailto commands for

### Trello Api Key

The API key for your target Trello account

### Trello Token

The board token to be used with the Trello submits

### Lists

A list of Trello lists and the board's they belong to. This can be used with the Trello submit methods to target reports to specific lists in Trello such as having a list for each Bug, Feedback and Request and directing reports accordingly.

## Examples

### Capture Screen

This example captures all of the screen in a Texture2D object which can later be saved or used in the game. The callback paramiter is an Action\<Texture2D, bool> that will be called when the process completes. The Texture2D is the resulting image and the bool represents success.

```csharp
FeedbackSystem.Screenshot.Capture(callback);
```

### Capture Rect

This example captures a section of the screen in a Texture2D object which can later be saved or used in the game. The callback parameter is an Action\<Texture2D, bool> that will be called when the process completes. The Texture2D is the resulting image and the bool reprints success.

```csharp
FeedbackSystem.Screenshot.Capture(fromPixel, toPixel, callback);
```

### Save Image

The callback is an Action\<string, bool> that will be called when the process completes. The string indicates the full file path of the resulting image and the boolean represents success or failure.

#### Capture Screen and Save JPG

```csharp
FeedbackSystem.Screenshot.SaveJpg(fileName, callback);
```

#### Capture Screen and Save PNG

```csharp
FeedbackSystem.Screenshot.SavePng(fileName, callback);
```

#### Capture Rect and Save JPG

fromPixel is a VectorInt2 being the pixel space to start the rect at while toPixel is the VectorInt2 being the pixel space to end the rect at. The system will force From to be less than To

```csharp
FeedbackSystem.Screenshot.SaveJpg(fromPixel, toPixel, fileName, callback);
```

#### Capture Rect and Save Png

fromPixel is a VectorInt2 being the pixel space to start the rect at while toPixel is the VectorInt2 being the pixel space to end the rect at. The system will force From to be less than To

```csharp
FeedbackSystem.Screenshot.SavePng(fromPixel, toPixel, fileName, callback);
```

#### Save Texture2D as JPG

This assumes the image you wish to save is stored as a Texture2D named texture

```csharp
FeedbackSystem.Screenshot.SaveJpg(fileName, path, texture, callback);
```

#### Save Texture2D as PNG

This assumes the image you wish to save is stored as a Texture2D named texture

```csharp
FeedbackSystem.Screenshot.SaveJpg(fileName, path, texture, callback);
```

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
Path is an optional parameter that if left null or omitted the system will save the log to the persistent data path as defined by the Unity Engine. Where exactly this is depends on the platform.
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

### Submit Email

A simple mail to command that will for most platforms open the default email tool and prepopulate the subject and body of the email.

{% hint style="info" %}
Due to limitations of various systems and email tools it is not possible to pre-attach files in a reliable way. The recommendation is to ask the user to attach any saved files them selves.
{% endhint %}

```csharp
FeedbackSystem.EmailSubmit(subject, body);
```

### Submit Trello

{% hint style="warning" %}
Heathen Engineering is not a partner of Trello nor are we recommending its use. The integration with Trello is provided as is. For support, questions about or general inquires pertaining to Trello please contact Trello.
{% endhint %}

This will create an entry on the target Trello account.

| Type                         | Paramiter   | Use                                                                                                                                               |
| ---------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| string                       | title       | The title of the card to be created on the list                                                                                                   |
| string                       | markdown    | The markdown content to be added as the card's description                                                                                        |
| int                          | list        | The index of the list the card should be added to. The specifics of this list are defined in the Feedback Configuration file linked to the system |
| IEnumerable\<string>         | attachments | A collection of file paths to be attached to the card e.g. the log file path, screen shot file path, etc.                                         |
| Action\<Trello.ActionStatus> | callback    | A callback to be invoked then the process completes that will indicate the status of the process                                                  |

```csharp
StartCoroutine(FeedbackSystem.TrelloSubmit(
    title,
    markdown,
    list,
    attachments,
    callback);
```

### 3rd Party Support Tools

You can use the Feedback system with 3rd party support tools such as Zendesk to better inform your support team.

{% hint style="info" %}
Zendesk is used in this example as its known to have a Unity integration making it trivial to integrate your game with your Zendesk support portal. The following examples show how you might use the User eXperience log data to enrich that integration.
{% endhint %}

{% hint style="danger" %}
Heathen Engineering is not a partner with Zendesk nor are we recommending you use Zendesk. Zendesk is simply used in this example to show how you may use Heathen's User eXperience Feedback tools with 3rd parties such as Zendesk.

For support, questions about or general inquiries relating to Zendesk, please contact Zendesk.
{% endhint %}

Lets assume you are using Zendesk as your support tool provider and you have integrated Zendesk with your game for a direct user support experience. In the case of support requests Zendesk allows you to define custom fields and these fields can be made invisible to the Support Request form which makes since for system data that isn't meant to be edited by a user but is useful for the support agent to know

{% embed url="https://developer.zendesk.com/documentation/classic-sdks/unity-native-sdk/unity-sdk/support/#support-requests" %}

For this example lets assume you have created custom fields as such

| Field ID | Type    | Use              |
| -------- | ------- | ---------------- |
| 1        | text    | Company Name     |
| 2        | text    | Product Name     |
| 3        | text    | Product Version  |
| 4        | text    | Engine Version   |
| 5        | text    | Command Line     |
| 6        | text    | Platform         |
| 7        | text    | Device Type      |
| 8        | text    | Device Model     |
| 9        | text    | Device Name      |
| 10       | text    | OS               |
| 11       | text    | OS Family        |
| 12       | text    | CPU Type         |
| 13       | numeric | CPU Count        |
| 14       | numeric | CPU Frequency    |
| 15       | numeric | System Memory    |
| 16       | text    | GPU Vendor       |
| 17       | text    | GPU Type         |
| 18       | text    | GPU Name         |
| 19       | text    | GPU Version      |
| 20       | numeric | GPU Memory       |
| 21       | numeric | GPU Shader Level |

You can now record the system data gathered by the custom log&#x20;

```csharp
Dictionary<long,string> invisibleCustomFields = new Dictionary<long,string>;

invisibleCustomFields.Add(1,FeedbackSystem.Log.companyName);
invisibleCustomFields.Add(2,FeedbackSystem.Log.productName);
invisibleCustomFields.Add(3,FeedbackSystem.Log.productVersion);
invisibleCustomFields.Add(4,FeedbackSystem.Log.engineVersion);
invisibleCustomFields.Add(5,FeedbackSystem.Log.commandLine);
invisibleCustomFields.Add(6,FeedbackSystem.Log.platform);
invisibleCustomFields.Add(7,FeedbackSystem.Log.deviceType);
invisibleCustomFields.Add(8,FeedbackSystem.Log.deviceModel);
invisibleCustomFields.Add(9,FeedbackSystem.Log.deviceName);
invisibleCustomFields.Add(10,FeedbackSystem.Log.os);
invisibleCustomFields.Add(11,FeedbackSystem.Log.osFamily);
invisibleCustomFields.Add(12,FeedbackSystem.Log.cpuType);
invisibleCustomFields.Add(13,FeedbackSystem.Log.cpuCount);
invisibleCustomFields.Add(14,FeedbackSystem.Log.cpuFrequency);
invisibleCustomFields.Add(15,FeedbackSystem.Log.systemMemory);
invisibleCustomFields.Add(16,FeedbackSystem.Log.gpuVendor);
invisibleCustomFields.Add(17,FeedbackSystem.Log.gpuType);
invisibleCustomFields.Add(18,FeedbackSystem.Log.gpuName);
invisibleCustomFields.Add(19,FeedbackSystem.Log.gpuVersion);
invisibleCustomFields.Add(20,FeedbackSystem.Log.gpuMemory);
invisibleCustomFields.Add(21,FeedbackSystem.Log.gpuShaderLevel);

zendeskSupportUI.SetInvisibleCustomFields(invisibleCustomFields);
```
