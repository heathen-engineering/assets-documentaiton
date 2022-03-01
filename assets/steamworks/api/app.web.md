# App.Web

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/integration/steamworks-v2-complete-190316)asset.
{% endhint %}

## Introduction

### Namespace

```csharp
using AppWeb = HeathenEngineering.SteamworksIntegraiton.API.App.Web;
```

### Definition

```csharp
public static class App.Web
```

This leverages the ISteamApp interface from Valve's Steam Web API and exposes the features of that API in a C# and Unity centric way.

Note we do not attempt to expose authorized endpoints. That is much of the Steam Web API requires a publisher key and should be called from a trusted web server not from a game client or a game server. We only expose those web API calls that do not require a publisher key.

### What can it do?

The App Web interface can be used to read the news items from an App as they appear in Steam's backend such as patch notes and announcements and can also be used to find the published name of an app based on its app ID.
