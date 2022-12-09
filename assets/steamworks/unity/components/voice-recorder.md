# Voice Recorder



<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Meant to be attached to a game object representing the local player. This componenet helps capture voice data from the local user and prepare it for transmission.

## Definition

## Fields and Attributes

| Type  | Name         | Comments                                                                                                                        |
| ----- | ------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| float | bufferLength | The length of buffer in seconds range 0 to 1                                                                                    |
| bool  | IsRecording  | <p>Indicates rather or not the system is currently capturing audio.</p><p></p><p>this can be set to start or stop recording</p> |

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
