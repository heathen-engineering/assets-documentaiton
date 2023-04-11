---
description: Get player feedback with rich game data to help improve your game.
---

# Logging & Feedback

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="./">User eXperience Tools</a></td><td><a href="../ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

User eXperience kit helps you gather rich game data in a well formatted log, and then feed that data from within your game tools such as Trello, Zendesk, Unity's User Reporting, etc. and to help you capture and save screenshots for the full screen or sections of the screen.

![](<../../../../.gitbook/assets/image (92).png>)

## Features

### [Advanced Log](../../api/log.md)

A log system which stores all Debug.Log messages with optional stack trace information, and additional system information generated at run time. The log can be reported as a simple text log or serialized to a JSON object for easier programmatic processing.

### [Trello Integration](../../api/trello.md)

You can use the Trello integration to interact with Trello such as to create cards and upload attachments. Terllo is most useful for production feedback such as gathering feedback from closed testers and QC staff.

It is possible release with Trello integration but not advised as you risk exposing your Trello API Key and token.

### Unity User Reporting

Did you know Unity cloud services includes a flexible and easy to use User Reporting service? This service is well suited to gathering end user feedback and bug reports and can be easyily integrated with the Advanced Log and Screenshot interfaces.

{% embed url="https://unitytech.github.io/clouddiagnostics/userreporting/UnityCloudDiagnosticsUserReports.html" %}

### Easy 3rd Party Extension

The system is designed to be easily integrated with the reporting tools of your choice. The log produced can be exported as simple text or as a JSON object for easy parsing by other tools, and includes an easy to use Screenshot tool capable of capturing a full screen or any defined rect of a screen, and returning that data as a Texture2D or quickly saving it out as a Jpg or Png.

{% hint style="warning" %}
Remimber to Destroy(texture) your screenshot textures when your done with them.
{% endhint %}

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

For this example lets assume you have created custom fields in Zendesk as such

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
var logObject = API.Log.Object;
invisibleCustomFields.Add(1, logObject.companyName);
invisibleCustomFields.Add(2, logObject.productName);
invisibleCustomFields.Add(3, logObject.productVersion);
invisibleCustomFields.Add(4, logObject.engineVersion);
invisibleCustomFields.Add(5, logObject.commandLine);
invisibleCustomFields.Add(6, logObject.platform);
invisibleCustomFields.Add(7, logObject.deviceType);
invisibleCustomFields.Add(8, logObject.deviceModel);
invisibleCustomFields.Add(9, logObject.deviceName);
invisibleCustomFields.Add(10, logObject.os);
invisibleCustomFields.Add(11, logObject.osFamily);
invisibleCustomFields.Add(12, logObject.cpuType);
invisibleCustomFields.Add(13, logObject.cpuCount);
invisibleCustomFields.Add(14, logObject.cpuFrequency);
invisibleCustomFields.Add(15, logObject.systemMemory);
invisibleCustomFields.Add(16, logObject.gpuVendor);
invisibleCustomFields.Add(17, logObject.gpuType);
invisibleCustomFields.Add(18, logObject.gpuName);
invisibleCustomFields.Add(19, logObject.gpuVersion);
invisibleCustomFields.Add(20, logObject.gpuMemory);
invisibleCustomFields.Add(21, logObject.gpuShaderLevel);

zendeskSupportUI.SetInvisibleCustomFields(invisibleCustomFields);
```
