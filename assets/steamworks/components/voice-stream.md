# Voice Stream

## Introduction

Meant to be attached to a game object representing non-local players. It can be used to playback the audio streamed in from those "other" players.

## Definition

### Fields and Attributes

| Type             | Name             | Comments                                                                                                 |
| ---------------- | ---------------- | -------------------------------------------------------------------------------------------------------- |
| AudioSource      | outputSource     | The audio source to play audio through                                                                   |
| SampleRateMethod | sampleRateMethod | The method by which to calculate samplerate                                                              |
| uint             | customSampleRate | If using a custom sample rate, specify that rate here.                                                   |
| double           | encodingTime     | <p>The max length of the current streaming clip time. </p><p></p><p>This can be useful for debugging</p> |

### Methods

```csharp
public void PlayVoiceData();
```

Plays a recieved Steamworks Voice package through the output source.

```csharp
public void StopRecording();
```

Stops the recording process.
