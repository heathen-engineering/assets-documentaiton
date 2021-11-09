# Utilities

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
public static class API.Utilities
```

Utilities has a few fatures that are globally avialable regardless of build platform

```csharp
uint ip = API.Utilities.IPStringToUint(string address);
```

```csharp
string ip = API.Utilities.IPUintToString(uint address);
```

```csharp
byte[] ip = API.Utilities.IPStringToBytes(string address);
```

```csharp
byte[] buffer = API.Utilities.FlipImageBufferVertical(width, height, data);
```

Client features are available under the client interface

```csharp
API.Utilites.Client
```

### What can it do?

The utilties interface contains misc features that dont fit in well to other interfaces. It can flip images, convert IP addresses frm uint, to string and back again and test Steam client's various modes.

## How To

### IP Country

```csharp
var country = API.Utilities.Client.IpCountry;
```

### Seconds SInce App Active

```csharp
var seconds = API.Utilites.Client.SecondsSinceAppActive;
```

### Server Real Time

```csharp
var time = API.Utilites.Client.ServerRealTime;
```

### Steam UI Language

```csharp
var langauge = API.Utilities.Client.SteamUILanguage;
```

### Big Picture Mode

```csharp
var bigPicuture = API.Utilities.Client.IsSteamInBigPictureMode;
```

### In VR Mode

```csharp
var vrMode = API.Utilities.Client.IsSteamRunningInVR;
```

### In Steam Deck

```csharp
var deck = API.Utilities.Client.IsSteamRunningONSteamDeck;
```

### VR Streaming Enabled

```csharp
var VRStreaming = API.Utilities.Client.IsVRHeadsetStreamingenabled;
```
