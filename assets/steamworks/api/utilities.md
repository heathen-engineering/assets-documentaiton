# Utilities

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegration.API;
```

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

###
