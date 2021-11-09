# Voice

## Introduction

```csharp
public static class API.Voice
```

The whole of the voice system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Voice.Client
```

### What can it do?

capture, compress and decompress voice data.

### Related Componenets

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/voice-recorder" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/voice-stream" %}

## How To

### Optimal Sample Rate

```csharp
var rate = API.Voice.Client.OptimalSampleRate;
```

### Decompress Voice

```csharp
API.Voice.Client.DecompressVoice(data, buffer, out size, rate);
```

### Get Available Voice

```csharp
API.Voice.Client.GetAvailableVoice(out compressed);
```

### Get Voice

```csharp
API.Voice.Client.GetVoice(buffer, out written);
```

### Start Recording

```csharp
API.Voice.Client.StartRecording();
```

### Stop Recording

```csharp
API.Voice.Client.StopRecording();
```
