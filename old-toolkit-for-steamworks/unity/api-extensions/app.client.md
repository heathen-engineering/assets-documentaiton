---
description: Access the Steam App system with Heathen's Steam API
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# App.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

### Namespace

```csharp
using AppClient = HeathenEngineering.SteamworksIntegration.API.App.Client;
```

### Definition

```csharp
public static class App.Client
```

This leverages the ISteamApp interface from Valve's Steam Client API and exposes every feature of that API in a C# and Unity centric way. Beyond a simple API wrapper the App.Client class provides for basic API initalizations and runs the callback update. It is possible to run Steam API without Steamworks Behaviour using only this class.

```csharp
AppClient.Initialize(AppData appId);
```

This will cause the client API from Valve's Steam API to be initialized to the App ID provided and will start a background worker to run callbacks for you.

### What can it do?

The App interface can be used to verify ownership, check for DLC, VAC Ban and more. The main function commonly used in Unity games would be Dlc. You can fetch a list of all DLC, check for ownership of the DLC and more.

Most of this functionality is wrapped up in your SteamSettings making it even easier to leverage.

## Events

### EventDlcInstalled

This event is invoked when a DLC is installed and has a single parameter of type `DlcInstalled_t`. The type `DlcInstalled_t` is defined by [Valve here](https://partner.steamgames.com/doc/api/ISteamApps#DlcInstalled\_t).

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(Steamworks.DlcInstalled_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.App.Client.EventDlcInstalled.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.App.Client.EventDlcInstalled.RemoveListener(HandleEvent);
}
```

### EventNewUrlLaunchParameters

This event is raised after the user executes a steam URL with command line or query parameters such as \`steam://run/\<appId>?param1=value1; while the game is already running. The new params can be queried with the GetLaunchCommandLine and GetLaunchQueryParam methods.

This event has a single parameter of type `NewUrlLaunchParameters_t` which is defined by [Valve here](https://partner.steamgames.com/doc/api/ISteamApps#NewUrlLaunchParameters\_t).

You would add a Listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(Steamworks.NewUrlLaunchParameters_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.App.Client.EventNewUrlLaunchParameters.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.App.Client.EventNewUrlLaunchParameters.RemoveListener(HandleEvent);
}
```

### EventServersConnected

Called when a connections to the Steam back-end has been established. This means the Steam client now has a working connection to the Steam servers. Usually this will have occurred before the game has launched, and should only be seen if the user has dropped connection due to a networking issue or a Steam server update.

Assuming a handler in the form of

```csharp
private void HandleEvent()
{
}
```

Then you would register the event such as:

```csharp
API.App.Client.EventServersConnected.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.App.Client.EventServersConnected.RemoveListener(HandleEvent);
}
```

### EventServersDisconnected

Called if the client has lost connection to the Steam servers.\
Real-time services will be disabled until a matching EventServersConnected has been posted.

You can read more about the [EResult data type here](https://partner.steamgames.com/doc/api/steam\_api#EResult).

Assuming a handler in the form of

```csharp
private void HandleEvent(EResult result)
{
}
```

Then you would register the event such as:

```csharp
API.App.Client.EventServersDisconnected.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.App.Client.EventServersDisconnected.RemoveListener(HandleEvent);
}
```

### EventServersConnectFailure

Called when a connection attempt has failed. This will occur periodically if the Steam client is not connected, and has failed when retrying to establish a connection.

You can read more about the [SteamServerConnectFailure\_t data type here](https://partner.steamgames.com/doc/api/ISteamUser#SteamServerConnectFailure\_t).

Assuming a handler in the form of

```csharp
private void HandleEvent(SteamServerConnectFailure_t result)
{
}
```

Then you would register the event such as:

```csharp
API.App.Client.EventServersConnectFailure.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    API.App.Client.EventServersConnectFailure.RemoveListener(HandleEvent);
}
```

## Fields and Attributes

### Initialized

This is a global field located on API.App.Initalized and indicates rather or not the system is initialized.

{% hint style="info" %}
This is \***Not**\* located in the API.App.Client class rather its in the parent API.App class so to access it&#x20;

```csharp
if(API.App.Initialized)
    ;//Yes it is initalized
else
    ;//No it is not
```
{% endhint %}

```csharp
public static bool API.App.Initalized => get;
```

### LoggedOn

Indicates rather or not the system is logged on to the Steam backend services. When false this indicates the system is running in "offline mode" and as a result realtime systems like Lobby, parts of Inventory and others will not funciton or will have a limited level of funcitonality.

```csharp
public static bool LoggedOn => get;
```

### IsSubscribed

Check if the active user is subscribed to the current App ID ... in Valve's speak this means that the active user has a license to this app.

```csharp
public static bool IsSubscribed => get;
```

You can call this field via

```csharp
if(API.App.Client.IsSubscribed)
    Debug.Log("The user is subscribed");
else
    Debug.Log("The user is not subscribed");
```

### IsSubscribedFromFamilySharing

Checks if the active user is accessing the current appID via a temporary Family Shared license owned by another user.

```csharp
public static bool IsSubscribedFromFamilySharing => get;
```

You can call this field via

```csharp
if(API.App.Client.IsSubscribedFromFamilySharing)
    Debug.Log("The user is subscribed from family");
else
    Debug.Log("The user is not subscribed from family");
```

### IsSubscribedFromFreeWeekend

Checks if the user is subscribed to the current App ID through a free weekend.

```csharp
public static bool IsSubscribedFromFreeWeekend => get;
```

You can call this field via

```csharp
if(API.App.Client.IsSubscribedFromFreeWeekend)
    Debug.Log("The user is subscribed from free weekend");
else
    Debug.Log("The user is not subscribed from free weekend");
```

### IsVACBanned

Checks if the user has a VAC (Valve Anti Cheat) ban on their account

```csharp
public static bool IsVACBanned => get;
```

You can call this field via

```csharp
if(API.App.Client.IsVACBanned)
    Debug.Log("The user is Valve Anti Cheat banned");
else
    Debug.Log("The user is not Valve Anti Cheat banned");
```

### Owner

Gets the UserData for the owner of the app, if this is different than the local user then the app is being barrowed.

```csharp
public static UserData Owner => get;
```

You can call this field via

```csharp
var owner = API.App.Client.Owner;
Debug.Log("The owners name is " + owner.Name);
```

### AvailableLanguages

Returns a list of languages supported by the app

```csharp
public static string[] AvailableLanguages => get;
```

You can call this field via

```csharp
var languages = API.App.Client.AvailableLanguages;
Debug.Log("The app supports " + languages.Length + " langauges.");
```

### IsBeta

Returns true if a beta branch is being used

```csharp
public static bool IsBeta => get;
```

You can call this field via

```csharp
if(API.App.Client.IsBeta)
    Debug.Log("Is a beta build");
else
    Debug.Log("Is not a beta build");
```

### CurrentBetaName

Returns a list of languages supported by the app

```csharp
public static string CurrentBetaName => get;
```

You can call this field via

```csharp
var betaName = API.App.Client.CurrentBetaName;
Debug.Log(betaName);
```

### CurrentGameLanguage

Gets the current language that the user has set

```csharp
public static string CurrentGameLanguage => get;
```

You can call this field via

```csharp
var language = API.App.Client.CurrentGameLanguage;
Debug.Log(language);
```

### Dlc

Returns the metadata for all available DLC

```csharp
public static DlcData[] Dlc => get;
```

You can call this field via

```csharp
var dlcs = API.App.Client.Dlc;
Debug.Log("The app has " + dlcs.Length + " DLCs.");
```

### IsCybercafe

Checks whether the current App ID is for Cyber Cafes.

```csharp
public static bool IsCybercafe => get;
```

You can call this field via

```csharp
if(API.App.Client.IsCybercafe)
    Debug.Log("Is a cybercafe");
else
    Debug.Log("Is not a cybercafe");
```

### IsLowViolence

Checks if the license owned by the user provides low violence depots.

```csharp
public static bool IsLowViolence => get;
```

You can call this field via

```csharp
if(API.App.Client.IsLowViolence)
    Debug.Log("Is a low violence license");
else
    Debug.Log("Is not a low violence license");
```

### Id

Gets the App Id of the current process.

```csharp
public static AppId_t Id => get;
```

You can call this field via

```csharp
var appId = API.App.Client.CurrentGameLanguage;
Debug.Log(language);
```

### BuildId

Gets the build id (aka the Build Number) of this app, may change at any time based on backend updates to the game.

```csharp
public static int BuildId => get;
```

You can call this field via

```csharp
var build = API.App.Client.BuildId;
Debug.Log("Current build ID: " + build);
```

### InstallDirectory

Gets the buildid of this app, may change at any time based on backend updates to the game.

```csharp
public static string InstallDirectory => get;
```

You can call this field via

```csharp
var installDirectory = API.App.Client.InstallDirectory;
Debug.Log("Installed to folder: " + installDirectory);
```

### DLCCount

Gets the number of DLC pieces for the current app.

```csharp
public static int DLCCount => get;
```

You can call this field via

```csharp
var count = API.App.Client.DLCCount;
Debug.Log("DLC Count: " + count);
```

### LaunchCommandLine

Gets the command line if the game was launched via Steam URL, e.g. steam://run/\<appid>//\<command line>/. This method is preferable to launching with a command line via the operating system, which can be a security risk. In order for rich presence joins to go through this and not be placed on the OS command line, you must enable "Use launch command line" from the Installation > General page on your app.

```csharp
public static string LaunchCommandLine => get;
```

You can call this field via

```csharp
var commandLine = API.App.Client.LaunchCommandLine;
Debug.Log("Command Line: " + commandLine);
```

## Methods

### Initialize

Initializes the the Steam API for client processing. If your using SteamSettings or SteamworksBehaviour this is done for you. You should only call this if you are not using SteamSettings.Initialize or SteamworksBehaviour.

```csharp
public static Initialize(AppData appId);
```

### IsAppInstalled

Checks if a specific app is installed.&#x20;

The app may not actually be owned by the current user, they may have it left over from a free weekend, etc. This only works for base applications, not Downloadable Content(DLC). Use IsDlcInstalled for DLC instead.

```csharp
public static bool IsAppInstalled(AppId_t appId);
```

### IsDlcInstalled

Checks if the user owns a specific DLC and if the DLC is installed

```csharp
public static bool IsDlcInstalled(AppId_t appId);
```

### GetDlcDownloadProgress

Gets the download progress for optional DLC.

```csharp
public static bool GetDlcDownloadProgress(AppId_t appId, 
                                out ulong bytesDownloaded, 
                                out ulong bytesTotal);
```

### GetAppInstallDirectory

Gets the install directory of the app if any

```csharp
public static string GetAppInstallDirectory(AppId_t appId);
```

### InstalledDepots

Returns the collection of installed depots in mount order

```csharp
public static DepotId_t[] InstalledDepots(AppId_t appId);
```

### QueryLaunchParam

Parameter names starting with the character '@' are reserved for internal use and will always return an empty string. Parameter names starting with an underscore '\_' are reserved for steam features -- they can be queried by the game, but it is advised that you not param names beginning with an underscore for your own features.

```csharp
public static string QueryLaunchParam(string key);
```

### InstallDLC

Install an optional DLC

```csharp
public static void InstallDLC(AppId_t appId);
```

### UninstallDLC

Uninstall an optional DLC

```csharp
public static void UninstallDLC(AppId_t appId);
```

### IsSubscribedApp

Checks if the active user is subscribed to a specified appId.

```csharp
public static bool IsSubscribedApp(AppId_t appId);
```

### IsTimedTrial

Is the current license a time trial license

```csharp
public static bool IsTimedTrial(out uint secondsAllowed, out uint secondsPlayed);
```

### GetCurrectBetaName

Gets the current beta branch name if any

```csharp
public static bool GetCurrentBetaName(out string name);
```

### GetEarliestPurchaseTime

Gets the time of purchase of the specified app

```csharp
public static DateTime GetEarliestPurchaseTime(AppId_t appId);
```

### GetFileDetails

Asynchronously retrieves metadata details about a specific file in the depot manifest.

```csharp
public static void GetFileDetails(string name, 
                Action<FileDetailsResult_t, bool> callback);
```

### MarkContentCorrupt

If you detect the game is out-of-date (for example, by having the client detect a version mismatch with a server), you can call use MarkContentCorrupt to force a verify, show a message to the user, and then quit.

```csharp
public static bool MarkContentCorrupt(bool missingFilesOnly);
```

## How To

### Check if Online

You can check if the user is currently connected to the Steam backend as a good means to check if the user is "online" at least as far as Steam is concenred.

```csharp
if(API.App.Client.LoggedOn)
    Debug.Log("Yes they are connected");
else
    Debug.Log("no they are not connected");
```

The events [EventServersConnected ](app.client.md#eventserversconnected)and [EventServersDisconnected](app.client.md#eventserversdisconnected) will be invoked as the connection is gained or lost respectively.

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
2. The local user is authenticated to Steam and has a legit path to play your game
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

The App interface can check the local user's VAC Ban status via

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

You can also fetch the current game language

```csharp
string currentLanguage = API.App.CurrentGameLanguage;
```

### Check for beta status

The App interface can check if the current build is a beta and if so which one.

```csharp
if(API.App.Client.IsBeta)
    Debug.Log("They are helping us test!");
```

Alternatively

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

The returned DownloadableContent objects can further be used to check for ownership and install of a given DLC. Again you would typically do this from your Steam Settings which will already have this information to hand but this can be useful when you want or need to check DLC availability at runtime.

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

Getting a specific launch parameter can be done with :

```csharp
string param = API.App.Client.QueryLaunchParam(key);
```

While rare it is possible that the user would have tried to relaunch the game with different launch parameters. You can monitor the new URL launch parameters event to react to this case.

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

If you detect that an update is needed you can mark the project as corrupted forcing Steam client to check for and download the content as needed

```csharp
API.App.Client.MarkContentCorrupt(checkMissingFilesOnly);
```
