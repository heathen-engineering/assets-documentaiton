# Voice

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../">Guides and Tutorials</a></td><td><a href="../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../assets/physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../assets/ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% embed url="https://partner.steamgames.com/doc/features/voice" %}

Steam Voice helps you record voice data from the local user and prepare it for sending. It also helps you consume that data and play it back.

Steam Voice does not deal with the sending of data. How you choose to send data from one user to another is a matter of how you handle networking in your game. Steam does provide networking tools or you can use any other networking solution you might like.

## Tools

Heathen's Steamworks Complete includes two tools to simplify the process of capturing and playing back voice data.

### [Voice Recorder](../../../assets/steamworks/unity/components/voice-recorder.md)

The [voice recorder componenet](../../../assets/steamworks/unity/components/voice-recorder.md) can be used to capture the local user's voice data and prepare it for transmission over your network connection. It provides the data via a [simple event](../../../assets/steamworks/unity/components/voice-recorder.md#evtvoicestream) feeding a byte\[] of data that should be easily handled by any networking solution.

The idea is that you connect the Voice Stream event up to a method that can send that data over your network.

![](<../../../.gitbook/assets/image (158) (1) (1).png>)

```csharp
voiceRecorded.evtVoiceStream.AddListener(SendVoiceData);
```

The [Voice Stream](../../../assets/steamworks/unity/components/voice-recorder.md#evtvoicestream) event gets invoked when the buffer is full and ready for transmission.

### [Voice Stream](../../../assets/steamworks/unity/components/voice-stream.md)

![](<../../../.gitbook/assets/image (187) (1) (1) (1).png>)

The [voice stream componenet](../../../assets/steamworks/unity/components/voice-stream.md) can be used to play back voice data produced by the voice recorded component. The intent is that your network system receiving voice data from a Voice Recorded would call the [Play Voice Data method](../../../assets/steamworks/unity/components/voice-stream.md#play-voice-data) on this component.

Typically you would have one [voice stream componenet](../../../assets/steamworks/unity/components/voice-stream.md) per connected player (excluding the local player) you can attach these voice stream components to the player's character or controller such that voice audio can (optionally) be accurately represented as 3D audio.
