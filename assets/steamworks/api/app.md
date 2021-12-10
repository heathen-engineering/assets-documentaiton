---
description: Access the Steam App system with Heathen's Steam API
---

# App

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegraiton.API;
```

```csharp
public static class API.App
```

The whole of the app system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.App.Client
```

### What can it do?

The App interface can be used to varify ownership, check for DLC, VAC Ban and more. The main funciton commonly used in Unity games would be Dlc. You can fetch a list of all DLC, check for ownership of the DLC and more.

Most of this funcitonality is wrapped up in your SteamSettings making it even easier to leverage.

## How To

### Check for app ownership

You can check if the user owns the current app via

```csharp
if(API.App.Client.IsSubscribed)
    Debug.Log("Yes they own it");
else
    Debug.Log("no they do not own it");
```

There are multiple ways for a user to have legitimate access to your game however so this alone doesn't always tell the full story. For example your player may be barrowing the game from a Steam  Family Sharing link.

```csharp
if(API.App.Client.IsSubscribedFromFamilySharing)
    Debug.Log("Share and share alike");
```

or perhaps you offered your game via a free weekend promotion

```csharp
if(API.App.Client.IsSubscribedFromFreeWeekend)
    Debug.Log("Your promotion is working!");
```

Time trials are another option

```csharp
if(API.App.Client.TimedTrial(out uint secondsAllowed, out uint secondsPlayed))
{
    Debug.Log("Time bomb detected, " + 
    (secondsAllowed - secondsPlayed) + " seconds remaining");
}
```

Your game could be, being played via a Cybercafe

```csharp
if(API.App.Client.IsCybercafe)
    Debug.Log("Supporting small buisness");
```

Finally you may just want to see who the proper owner of this license is

```csharp
UserData user = API.App.Client.Owner;
```

If the owner doesn't match the current user then you know several things

1. The local user is interested in game and has either barrowed it from a family member, is playing it via a promotion such as a free weekend or is playing it at a Cybercafe
2. The local user is authenitcated to Steam and has a legit path to play your game
3. The owner of the game has in one way or another promoted your game for you ... you could use that to drive a reward system or simply make note of it for your own marketing&#x20;

```csharp
if(API.App.Client.Owner != API.User.Client.Id)
    Debug.Log("Legit user, we should try to market to");
```

### Check purchase date

Check when the user first purchased the game (or any app), if you get a date back from the 70s then they purchased the game before Steam started tracking ... or they never purchased the game.

```csharp
DateTime purchaseDate = API.App.Client.GetEarliestPurchaseTime(API.App.Id);    
```

### Check for VAC Ban

The App interface can cehck the local user's VAC Ban status via

```csharp
if(API.App.Client.IsVACBanned)
    Debug.Log("Naughty player is naughty");
```

### Check language

The App interface is able to list the available languages for this app from Steam

```csharp
foreach(var language in API.App.Client.AvailableLanguages)
{
    Debug.Log(language + " is available.");
}
```

You can also fetch thhe current game language

```csharp
string currentLanguage = API.App.CurrentGameLanguage;
```

### Check for beta status

The App interface can check if the current build is a beta and if so which one.

```csharp
if(API.App.Client.IsBeta)
    Debug.Log("They are helping us test!");
```

Alternativly

```csharp
string betaName = API.App.Client.CurrentBetaName;

if(!string.IsNullOrEmpty(betaName))
    Debug.Log("They are helping us test in beta " + betaName);
else
    Debug.Log("An empty beta name tells us its not a beta");
```

### Get available DLC

Typically you would have done this at development time but you can query for a list of all DLC available to this app at run time.

```csharp
foreach(var dlc in API.App.Client.Dlc)
{
    Debug.Log(dlc.Name + " is a DLC availabel to this player");
}
```

The returned DownloadableContent objects can further be used to check for ownership and install of a given DLC. Again you would typically do this from your Steam Settings whcih will already have this information to hand but this can be useful when you want or need to check DLC availability at runtime.

### Check DLC Ownership

You can also check for ownership of any related app ID

```csharp
if(API.App.Client.IsSubscribedApp(appId))
    Debug.Log("They own it");
```

### Check DLC Install

While most modern DLC dont need to install, typically a game always contains all of its content especially if its multiplayer. DLC ownership typically only unlocks the content for the player. That said a DLC is an app and can download new content ... to check for the install of that content use:

Even if your DLC is empty it can still be useful to test this to see if they have the DLC enabled. Some gamers will disable DLC to play the vanilla version that would cause ownership to be true but install to be false.

```csharp
if(API.App.Client.IsDlcInstalled(dlcId))
    Debug.Log("They both own and have installed this DLC");
```

### Get DLC Download Progress

DLC can be installed or uninstalled from within game, to check the status of the install/download progress use:

```csharp
if(API.App.Client.GetDlcDownloadProgress(dlcId, out ulong downloaded, out ulong total))
    Debug.Log((downloaded /(float)total).ToString("P") + " complete");
```

### Install a DLC

To start a DLC install process

```csharp
API.App.Client.InstallDLC(dlcId);
```

You can monitor the installed event to know when the install is complete

```csharp
API.App.Client.EventDlcInstalled.AddListener(HandleDlcInstalled);
```

### Uninstall a DLC

To uninstall a DLC

```
API.App.Client.UninstallDLC(dlcId);
```

### Get app and depot information

You can also use the App interface to check for depot and file data for a given app.

```csharp
if(API.App.Client.IsAppInstalled(appid))
    Debug.Log("That app is installed");
```

Understanding where an app is installed can be of use

```csharp
string directory = API.App.Client.GetAppInstallDirectory(appid);
```

Getting a list of the depots that are installed for an app can be done with:

```csharp
foreach(var depotId in API.App.Client.InstalledDepoty(appId))
{
    //...
}
```

You can return the command line the app was launched with&#x20;

```csharp
string commandLine = API.App.Client.LaunchCommandLine;
```

Getting a specific launch paramiter can be done with :

```csharp
string param = API.App.Client.QueryLaunchParam(key);
```

While rare it is possible that the user would have tried to relaunch the game with different launch paramiters. You can monitor the new URL launch parameters event to react to this case.

```csharp
API.App.Client.EventNewUrlLaunchParameters.AddListener(HandleNewUrlParams);
```

### Checking file details

Many online games require that the game is up to date, you can fetch the details of a particular file.

```csharp
API.App.Client.GetFileDetails(fileName, (results, IOError) =>
{
    //...
});
```

If you detect that an update is needed you can mark the project as corupted forcing Steam client to check for and download the content as needed

```csharp
API.App.Client.MarkContentCorrupt(checkMissingFilesOnly);
```
