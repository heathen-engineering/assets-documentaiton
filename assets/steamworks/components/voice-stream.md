# Voice Stream

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

Meant to be attached to a game object representing non-local players. It can be used to playback the audio streamed in from those "other" players.

## Definition

## Fields and Attributes

| Type             | Name             | Comments                                                                                                 |
| ---------------- | ---------------- | -------------------------------------------------------------------------------------------------------- |
| AudioSource      | outputSource     | The audio source to play audio through                                                                   |
| SampleRateMethod | sampleRateMethod | The method by which to calculate samplerate                                                              |
| uint             | customSampleRate | If using a custom sample rate, specify that rate here.                                                   |
| double           | encodingTime     | <p>The max length of the current streaming clip time. </p><p></p><p>This can be useful for debugging</p> |

## Methods

### Play Voice Data

```csharp
public void PlayVoiceData(buffer);
```

Plays a recieved Steamworks Voice package through the output source.
