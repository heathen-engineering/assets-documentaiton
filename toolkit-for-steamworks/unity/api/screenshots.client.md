---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Screenshots.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using Screenshots = HeathenEngineering.SteamworksIntegration.API.Screenshots.Client;
```

```csharp
public static class Screenshots.Client
```

### What can it do?

Take screenshots ... that is the main function hence the name

The main reason to use this is if your handling your own advanced screenshot features ... as is all the rage these days.

You can enabled the HookScreenshots feature and Steam will notify you when the user hits the screenshot button they have configured in Steam client. You can then start the process of taking the screenshot however makes since for your game.

## Events

### Screenshot Ready

A screenshot successfully written or otherwise added to the library and can now be tagged.

### Screenshot Requested

A screenshot has been requested by the user from the Steam screenshot hotkey. This will only be called if HookScreenshots has been enabled, in which case Steam will not take the screenshot itself.

## How To

### Hook Screenshots

Ever wanted to do a fancy screenshot mode for your game, so every screenshot a player takes looks perfect and bug free and is effectively free marketing?

Well the first trick is to actually create such a system, that is left up to you but we recommend using tools like Time Line Director, Cinamachine, Post Processing Volumes, etc.

Next you need to catch the user's request to take a screenshot and trigger your system as opposed to letting the overlay or similar capture the screen.

```csharp
API.Screenshots.Client.IsScreenshotHooked = true;
```

once done Steam will no longer take screenshots when the user presses the configured screenshot button instead the EventScreenshotRequested event will trigger so you should register to that and act accordingly.

```csharp
API.Screenshots.Client.EventScreenshotRequested.AddListener(HandleScreenshot);
```

### Manage Screenshots

Once you have taken a screenshot you need to add it to the Steam screenshot library and possibly tag and update it.

```csharp
var handle = API.Screenshots.Client.AddScreenshotToLibrary(file, thumbnail, width, height);
```

The handle returned can be used to perform additional operations

```csharp
API.Screenshots.Client.SetLocation(handle, location);
```

```csharp
API.Screenshots.Client.TagPublishedFile(handle, ugcFile);
```

```csharp
API.Screenshots.Client.TagUser(handle, user);
```

### Take Screenshots

Alternatively you could request Steam to take a screenshot at key points in your game.

```csharp
var handle = API.Screenshots.Client.TriggerScreenshot();
```
