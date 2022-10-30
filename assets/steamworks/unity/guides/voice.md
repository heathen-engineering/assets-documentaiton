# Voice

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% embed url="https://partner.steamgames.com/doc/features/voice" %}

Steam Voice helps you record voice data from the local user and prepare it for sending. It also helps you consume that data and play it back.

Steam Voice does not deal with the sending of data. How you choose to send data from one user to another is a matter of how you handle networking in your game. Steam does provide networking tools or you can use any other networking solution you might like.

## Tools

Heathen's Steamworks Complete includes two tools to simplify the process of capturing and playing back voice data.

### [Voice Recorder](../components/voice-recorder.md)

The [voice recorder componenet](../components/voice-recorder.md) can be used to capture the local user's voice data and prepare it for transmission over your network connection. It provides the data via a [simple event](../components/voice-recorder.md#evtvoicestream) feeding a byte\[] of data that should be easily handled by any networking solution.

The idea is that you connect the Voice Stream event up to a method that can send that data over your network.

![](<../../../../.gitbook/assets/image (158) (1) (1).png>)

```csharp
voiceRecorded.evtVoiceStream.AddListener(SendVoiceData);
```

The [Voice Stream](../components/voice-recorder.md#evtvoicestream) event gets invoked when the buffer is full and ready for transmission.

### [Voice Stream](../components/voice-stream.md)

![](<../../../../.gitbook/assets/image (187) (1) (1) (1).png>)

The [voice stream componenet](../components/voice-stream.md) can be used to play back voice data produced by the voice recorded component. The intent is that your network system receiving voice data from a Voice Recorded would call the [Play Voice Data method](../components/voice-stream.md#play-voice-data) on this component.

Typically you would have one [voice stream componenet](../components/voice-stream.md) per connected player (excluding the local player) you can attach these voice stream components to the player's character or controller such that voice audio can (optionally) be accurately represented as 3D audio.
