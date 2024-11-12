---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Voice Recorder

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Meant to be attached to a game object representing the local player. This componenet helps capture voice data from the local user and prepare it for transmission.

## Definition

## Fields and Attributes

<table><thead><tr><th width="217.91333012691814">Type</th><th>Name</th><th width="316.8664058133036">Comments</th></tr></thead><tbody><tr><td>float</td><td>bufferLength</td><td>The length of buffer in seconds range 0 to 1</td></tr><tr><td>bool </td><td>IsRecording</td><td><p>Indicates rather or not the system is currently capturing audio.</p><p></p><p>this can be set to start or stop recording</p></td></tr></tbody></table>

## Events

### evtStopedOnChatRestricted

Occurs if voice recording is stoped due to being chat restricted

### evtVoiceStream

Occurs when the buffer is ready to send another load of data and will contain the byte\[] of compressed data to send. This should be hooked up to your networking solution to send the data to other users.

## Methods

### Start Recording

```csharp
public void StartRecording();
```

Starts the recording process.

### Stop Recording

```csharp
public void StopRecording();
```

Stops the recording process.
