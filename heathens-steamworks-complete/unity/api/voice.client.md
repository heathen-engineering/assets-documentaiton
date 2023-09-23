# Voice.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using SteamVoice = HeathenEngineering.SteamworksIntegration.API.Voice.Client;
```

```csharp
public static class Voice.Client
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
