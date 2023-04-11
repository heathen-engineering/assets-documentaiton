# Voice Recorder

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

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
