---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Voice Stream

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Meant to be attached to a game object representing non-local players. It can be used to playback the audio streamed in from those "other" players.

## Definition

## Fields and Attributes

<table><thead><tr><th width="217.91333012691814">Type</th><th>Name</th><th width="316.8664058133036">Comments</th></tr></thead><tbody><tr><td>AudioSource</td><td>outputSource</td><td>The audio source to play audio through</td></tr><tr><td>SampleRateMethod</td><td>sampleRateMethod</td><td>The method by which to calculate samplerate</td></tr><tr><td>uint</td><td>customSampleRate</td><td>If using a custom sample rate, specify that rate here.</td></tr><tr><td>double</td><td>encodingTime</td><td><p>The max length of the current streaming clip time. </p><p></p><p>This can be useful for debugging</p></td></tr></tbody></table>

## Methods

### Play Voice Data

```csharp
public void PlayVoiceData(buffer);
```

Plays a recieved Steamworks Voice package through the output source.
