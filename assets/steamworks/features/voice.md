---
description: Feature is here now, Documentation Coming Soon!
---

# Voice

## Introduction

Steam Voice is a feature of the Steam API which helps you capture audio from the player’s microphone and prepare it for transmission over a network. Similarly, it can help decode received voice data and make it ready for playback.

{% hint style="warning" %}
Steam Voice does not handle the send / receive of the data, its just responsible for capturing and then compressing and decompressing the audio; its up to you to handle sending the audio and feeding the resulting audio to the proper source.
{% endhint %}

Heathen Engineering’s SteamworksVoiceManager takes Steam Voice a step further and helps you capture the audio and play back received audio through a target audio source in Unity.

## Mirror Example

Typically you would attach this to the User’s player controller (such as in a Mirror Network Environment) along with an Audio Source which will be used to play back audio for listening users. When the object is spawned it would test for authority e.g. we check to see if this instance belongs to the local player. If so we will connect the “VoiceStream” event to a CMD to send the voice data up to the game server for example

```csharp
public class VoicedPlayerController : NetworkBehaviour
{
    //Make sure there is a SteamworksVoiceManager on this object
    private SteamworksVoiceManager voiceManager;

    private void Start()
    {
        //This is only called on the client that has authority over this
        //So we get the voice manager from this game object
        voiceManager = GetComponent<SteamworksVoiceManager>();
        if(hasAuthority)
        {
            //And set the listener on the voice stream event
            voiceManager.evtVoiceStream.AddListener(CmdSendVoiceStream);
        }
    }

    [Command]
    public void CmdSendVoiceStream(byte[] data)
    {
        if(data != null and data.lenght > 0)
        {
            //Send the received data to all clients
            RpcRecieveVoiceStream(data);
        }
    }

    [ClientRpc]
    public void RpcRecieveVoiceStream(byte[] data)
    {
        if (!hasAuthority)
        {
            //This is not the local player so we should play this audio
            voiceManager.PlayVoiceData(data);
        }
        else
        {
            //This is the audio I sent ... I dont need to hear it
        }
    }
}
```

In the above you can see that assume a SteamworksVoiceManager is on the player controller object. For the authority e.g. the local user that owns this we get the SteamworksVoiceManager and connect to its `evtVoiceStream` event. This means that when we start `StartRecording` the output will feed directly into our `CmdSendVoiceStream` the server will then feed that back over the `RpcRecieveVoiceStream` call and for users that are not the host they will play that audio.

With this method it is possible to do positional audio e.g. have the audio source play back with some degree of 3D positioning.

{% embed url="https://heathen-engineering.github.io/steamworks-v2-documentation/index.html#CSharpClass:HeathenEngineering.SteamAPI.SteamworksVoiceManager" %}

