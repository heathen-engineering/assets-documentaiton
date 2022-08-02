# Voice Stream

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
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
