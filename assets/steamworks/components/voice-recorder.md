# Voice Recorder

## Introduction

Meant to be attached to a game object representing the local player. This componenet helps capture voice data from the local user and prepare it for transmission.

## Definition

### Fields and Attributes

| Type  | Name         | Comments                                                                                                                        |
| ----- | ------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| float | bufferLength | The length of buffer in seconds range 0 to 1                                                                                    |
| bool  | IsRecording  | <p>Indicates rather or not the system is currently capturing audio.</p><p></p><p>this can be set to start or stop recording</p> |

### Events

#### Stoped On Chat Restricted

Occurs if voice recording is stoped due to being chat restricted

#### Voice Stream

Occurs when the buffer is ready to send another load of data and will contain the byte\[] of compressed data to send. This should be hooked up to your networking solution to send the data to other users.

### Methods

```csharp
public void StartRecording();
```

Starts the recording process.

```csharp
public void StopRecording();
```

Stops the recording process.
