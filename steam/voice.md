# 🗣️ Voice

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% embed url="https://partner.steamgames.com/doc/features/voice" %}

Steam Voice helps you record voice data from the local user and prepare it for sending. It also helps you consume that data and play it back.

Steam Voice does not deal with the sending of data. How you choose to send data from one user to another is a matter of how you handle networking in your game. Steam does provide networking tools or you can use any other networking solution you might like.

## Unity

Heathen's Steamworks Complete includes two tools to simplify the process of capturing and playing back voice data.

{% embed url="https://www.youtube.com/watch?v=hscKkzfAoyI" %}

### [Voice Recorder](../toolkit-for-steamworks/unity/components/voice-recorder.md)

The [voice recorder component](../toolkit-for-steamworks/unity/components/voice-recorder.md) can be used to capture the local user's voice data and prepare it for transmission over your network connection. It provides the data via a [simple event](../toolkit-for-steamworks/unity/components/voice-recorder.md#evtvoicestream) feeding a byte\[] of data that should be easily handled by any networking solution.

The idea is that you connect the Voice Stream event to a method that can send that data over your network.

![](<../.gitbook/assets/image (158) (1) (1).png>)

```csharp
voiceRecorded.evtVoiceStream.AddListener(SendVoiceData);
```

The [Voice Stream](../toolkit-for-steamworks/unity/components/voice-recorder.md#evtvoicestream) event gets invoked when the buffer is full and ready for transmission.

### [Voice Stream](../toolkit-for-steamworks/unity/components/voice-stream.md)

![](<../.gitbook/assets/image (187) (1) (1) (1).png>)

The [voice stream component](../toolkit-for-steamworks/unity/components/voice-stream.md) can be used to play back voice data produced by the voice-recorded component. The intent is that your network system receiving voice data from a Voice Recorded would call the [Play Voice Data method](../toolkit-for-steamworks/unity/components/voice-stream.md#play-voice-data) on this component.

Typically you would have one [voice stream component](../toolkit-for-steamworks/unity/components/voice-stream.md) per connected player (excluding the local player) you can attach these voice stream components to the player's character or controller such that voice audio can (optionally) be accurately represented as 3D audio.

## Unreal

Heathen's Steamworks Complete exposes all the necessary features to get and play voice data to Unreal Blueprint Functions.

### System Testing

Before you try to get and use voice data you would want to know if there is any data available, this would depend on you starting and stopping voice recording as well.

[Stop](../toolkit-for-steamworks/unreal/blueprint-nodes/functions/stop-voice-recording.md), [Start](../toolkit-for-steamworks/unreal/blueprint-nodes/functions/start-voice-recording.md) and [Get Available Voice](../toolkit-for-steamworks/unreal/blueprint-nodes/functions/get-available-voice.md) can be used for this purpose.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>A simple example of getting voice data</p></figcaption></figure>

Steam API provides the necessary tools to get compressed voice audio from the player's active audio input device if any.

#### [Steam Get Voice](../toolkit-for-steamworks/unreal/blueprint-nodes/functions/get-voice.md)

The Steam Get Voice node will return a result indicating the state of the data and the data as a compressed array of bytes.

It up to you how you send this data to those that might want to play it back. In most cases you would send it to the server which would then echo it down to all appropriate players.

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>A simple example of getting and decoding audio for the network</p></figcaption></figure>

To Stream voice data it's up to you to receive the compressed data from whatever source you wish to playback from, typically this would be a server sending you the data.

### [Decompress Voice](../toolkit-for-steamworks/unreal/blueprint-nodes/functions/decompress-voice.md)

The Steam Decompress Voice node takes in the compressed data and is a reference to a Procedural Sound Wave. It will then load the received data and indicate the state of that process. Once completed you can simply play the Procedural Sound Wave as either 2D or 3D, this system will continue to queue new audio onto the sound wave as it is received.
