---
cover: ../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Unity Voice

Heathen's Steamworks Complete includes two tools to simplify the process of capturing and playing back voice data.

### [Voice Recorder](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-recorder.md)

The [voice recorder component](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-recorder.md) can be used to capture the local user's voice data and prepare it for transmission over your network connection. It provides the data via a [simple event](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-recorder.md#evtvoicestream) feeding a byte\[] of data that should be easily handled by any networking solution.

The idea is that you connect the Voice Stream event to a method that can send that data over your network.

![](<../../.gitbook/assets/image (158) (1) (1).png>)

```csharp
voiceRecorded.evtVoiceStream.AddListener(SendVoiceData);
```

The [Voice Stream](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-recorder.md#evtvoicestream) event gets invoked when the buffer is full and ready for transmission.

### [Voice Stream](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-stream.md)

![](<../../.gitbook/assets/image (187) (1) (1) (1).png>)

The [voice stream component](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-stream.md) can be used to play back voice data produced by the voice-recorded component. The intent is that your network system receiving voice data from a Voice Recorded would call the [Play Voice Data method](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-stream.md#play-voice-data) on this component.

Typically you would have one [voice stream component](../../heathens-toolkit-for-steamworks-sdk/unity/components/voice-stream.md) per connected player (excluding the local player) you can attach these voice stream components to the player's character or controller such that voice audio can (optionally) be accurately represented as 3D audio.
