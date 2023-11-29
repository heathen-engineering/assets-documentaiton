---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# Unreal Voice

## Introduction

Heathen's Steamworks Complete exposes all the necessary features to get and play voice data to Unreal Blueprint Functions.

## System Testing

Before you try to get and use voice data you would want to know if there is any data available, this would depend on you starting and stopping voice recording as well.

[Stop](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/stop-voice-recording.md), [Start](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/start-voice-recording.md) and [Get Available Voice](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/get-available-voice.md) can be used for this purpose.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## Get Voice

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption><p>A simple example of getting voice data</p></figcaption></figure>

Steam API provides the necessary tools to get compressed voice audio from the player's active audio input device if any.

### [Steam Get Voice](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/get-voice.md)

The Steam Get Voice node will return a result indicating the state of the data and the data as a compressed array of bytes.

It up to you how you send this data to those that might want to play it back. In most cases you would send it to the server which would then echo it down to all appropriate players.

## Stream Voice

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption><p>A simple example of getting and decoding audio for the network</p></figcaption></figure>

To Stream voice data it's up to you to receive the compressed data from whatever source you wish to playback from, typically this would be a server sending you the data.

### [Decompress Voice](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/decompress-voice.md)

The Steam Decompress Voice node takes in the compressed data and is a reference to a Procedural Sound Wave. It will then load the received data and indicate the state of that process. Once completed you can simply play the Procedural Sound Wave as either 2D or 3D, this system will continue to queue new audio onto the sound wave as it is received.
