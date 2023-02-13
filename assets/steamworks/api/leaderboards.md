# Leaderboards.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

```csharp
using Leaderboards = HeathenEngineering.SteamworksIntegration.API.Leaderboards.Client;
```

```csharp
public static class Leaderboards.Client;
```

To work with leaderboards from the point of view of a server you should use the Steam Web API for leaderboards.

{% embed url="https://partner.steamgames.com/doc/webapi/ISteamLeaderboards" %}

For more info on how to use the Steamworks Web API please see the [Web API Overview](https://partner.steamgames.com/doc/webapi\_overview).

### What can it do?

{% hint style="success" %}
See the [LeaderboardData ](https://kb.heathen.group/assets/steamworks/data-layer/leaderboard-data)struct, it can do most everything the raw API can do but is generally easier to work with.
{% endhint %}

Leaderboards are ranked lists of players where a player's score determines there position on the leaderboard. Leaderboards can contain additional data for each entry either as a details array or as an attachment, attachments are useful for playbacks and other large bits of information while details are useful for character builds, player settings, etc.

### Related Objects

{% embed url="https://kb.heathen.group/assets/steamworks/data-layer/leaderboard-data" %}

{% embed url="https://kb.heathen.group/assets/steamworks/for-unity-game-engine/scriptable-objects/leaderboard-object" %}

{% embed url="https://kb.heathen.group/assets/steamworks/for-unity-game-engine/components/leaderboard-manager" %}

{% embed url="https://kb.heathen.group/assets/steamworks/objects/leaderboard-entry" %}

{% embed url="https://kb.heathen.group/assets/steamworks/objects/rank-change" %}

## Fields and Attributes

### RequestTimeout

```csharp
public static float RequestTimeout { get; set; }
```

The amount of time a request will be waited on before it is considered timed out. If a request times out the callback provided will be invoked with a failed IO state i.g.

```csharp
//True indicates a IOError = true
callback?.Invoke(default, true);
```

### PendingSetUgcRequests

```csharp
public static int PendingSetUgcRequests { get; }
```

The number of Set UGC aka AttachUGC requests that are pending processing.

### PendingDownloadScoreRequests

```csharp
public static int PendingDownloadScoreRequests { get; }
```

The number of download score requests aka DownloadEntries that are pending processing

### PendingUploadScoreRequests

```csharp
public static int PendingUploadScoreRequests { get; }
```

The number of upload score requests aka UploadScore that are pending processing

## Methods

### AttachUGC

```csharp
public static void AttachUGC(LeaderboardData leaderboard, 
                             UGCHandle_t ugc, 
                             Action<LeaderboardUGCSet_t, bool> callback)
```

```csharp
public static void AttachUGC(LeaderboardData leaderboard, 
                             string fileName, 
                             byte[] data, 
                             Action<LeaderboardUGCSet_t, bool> callback)
```

```csharp
public static void AttachUGC(LeaderboardData leaderboard, 
                             string fileName, 
                             object jsonObject, 
                             System.Text.Encoding encoding, 
                             Action<LeaderboardUGCSet_t, bool> callback)
```

```csharp
public static void AttachUGC(LeaderboardData leaderboard, 
                             string fileName, 
                             string content, 
                             System.Text.Encoding encoding, 
                             Action<LeaderboardUGCSet_t, bool> callback)
```

{% hint style="info" %}
The callback deligate should be in the form of

```csharp
void CallbackHandler(LeaderboardUGCSet result, bool IOError);
```
{% endhint %}

This is used to attach complex data to the user's leaderboard entry. You can do so by providing an existing UGC item or by providing the data to be saved to UGC which will then be attached.

> [Valve Documentation](https://partner.steamgames.com/doc/api/ISteamUserStats#AttachLeaderboardUGC)
>
> Attaches a piece of user generated content the current user's entry on a leaderboard.\
> \
> This content could be a replay of the user achieving the score or a ghost to race against. The attached handle will be available when the entry is retrieved and can be accessed by other users using [GetDownloadedLeaderboardEntry](https://partner.steamgames.com/doc/api/ISteamUserStats#GetDownloadedLeaderboardEntry) which contains `LeaderboardEntry_t.m_hUGC`. To create and download user generated content see the documentation for the Steam Workshop.\
> \
> Once attached, the content will be available even if the underlying Cloud file is changed or deleted by the user.

### DownloadEntries

```csharp
public static void DownloadEntries(LeaderboardData leaderboard, 
                                   ELeaderboardDataRequest request, 
                                   int start, 
                                   int end, 
                                   int maxDetailsPerEntry, 
                                   Action<LeaderboardEntry[], bool> callback)
```

```csharp
public static void DownloadEntries(LeaderboardData leaderboard, 
                                   CSteamID[] users, 
                                   int maxDetailsPerEntry, 
                                   Action<LeaderboardEntry[], bool> callback)
```

```csharp
public static void DownloadEntries(LeaderboardData leaderboard, 
                                   UserData[] users, 
                                   int maxDetailsPerEntry, 
                                   Action<LeaderboardEntry[], bool> callback)
```

{% hint style="info" %}
The callback deligate should be in the form of

```csharp
void CallbackHandler(LeaderboardEntry[] result, bool IOError);
```
{% endhint %}

{% hint style="info" %}
[ELeaderboardDataRequest](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardDataRequest)

Documentation can be found at the link above.
{% endhint %}

This is used to query results from a leaderboard and is akin to the [`DownloadLeaderboardEntries`](https://partner.steamgames.com/doc/api/ISteamUserStats#DownloadLeaderboardEntries) and [`DownloadLeaderboardEntriesforUsers`](https://partner.steamgames.com/doc/api/ISteamUserStats#DownloadLeaderboardEntriesForUsers) from the raw Steam API.

> [Valve Documentation](https://partner.steamgames.com/doc/api/ISteamUserStats#DownloadLeaderboardEntries)
>
> Fetches a series of leaderboard entries for a specified leaderboard.
>
> You can ask for more entries than exist, then this will return as many as do exist.
>
> A maximum of 100 users can be downloaded at a time, with only one outstanding call at a time. If a user doesn't have an entry on the specified leaderboard, they won't be included in the result.

### Find

```csharp
public static void Find(string leaderboardName, 
                        Action<LeaderboardData, bool> callback)
```

{% hint style="info" %}
The callback deligate should be in the form of

```csharp
void CallbackHandler(LeaderboardData result, bool IOError);
```
{% endhint %}

The [Steamworks Behaviour](../unity/components/steamworks-behaviour.md) will call this for you as it initializes the Steam Settings and the boards you have defined within. You only need to call this your self if you are creating a build at run time manually and not using the [Leaderboard Object](../unity/scriptable-objects/leaderboard-object.md).

### GetDisplayType

```csharp
public static ELeaderboardDisplayType GetDisplayType(LeaderboardData leaderboard)
```

Gets the display type of the board from Valve's backend.

### GetEntryCount

```csharp
public static int GetEntryCount(SteamLeaderboard_t leaderboard)
```

Gets the number of entries recorded on this board

### GetName

```csharp
public static string GetName(SteamLeaderboard_t leaderboard)
```

Gets the name of the leaderboard as recorded on Valve's backend

### GetSortMethod

```csharp
public static ELeaderboardSortMethod GetSortMethod(SteamLeaderboard_t leaderboard)
```

Gets the sorting method used by this board as recorded on Valve's backend.

### UploadScore

```csharp
public static void UploadScore(SteamLeaderboard_t leaderboard, 
                               ELeaderboardUploadScoreMethod method, 
                               int score, 
                               int[] details, 
                               Action<LeaderboardScoreUploaded_t, bool> callback = null)
```

{% hint style="info" %}
The callback delegate should be in the form of

```csharp
void CallbackHandler(LeaderboardScoreUploaded_t result, bool IOError);
```
{% endhint %}

Uploads a score and optionally details for the user to the target leaderboard.

#### Parameters

* `SteamLeaderboard_t leaderboard`\
  The leaderboard to upload the score to
* `ELeaderboardUploadScoreMethod method`\
  The method to upload the score with ... see [This Article](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardUploadScoreMethod) for full details.
* `int score`\
  The score to be uploaded
* `int[] details`\
  An array of details, this cannot be longer than int\[64]. To read the details you must configure the desired length on your Leaderboard Object e.g. in you Steam Settings you must indicate how many detail entries the board's records will have.
* `Action<LeaderboardScoreUploaded_t, bool> callback`\
  A callback that will respond with the result

## How To

{% hint style="success" %}
The [Leaderboard ](../unity/scriptable-objects/leaderboard-object.md)object provides simplified access to many of the features found here in. Be sure to read the documentation for the [Leaderboard ](../unity/scriptable-objects/leaderboard-object.md)object to understand what options are available to you.
{% endhint %}

### Add an attachment

You can attach files to a user's leaderboard entry using the `AttachLeaderboardUGC` option. Attaches a piece of user generated content the current user's entry on a leaderboard. This content could be a replay of the user achieving the score or a ghost to race against.

```csharp
API.Leaderboards.Client.AttachUGC(board, ugc, callback);
```

{% hint style="info" %}
This requies you have a UGCHandle to the file you wish to attach. See the [Remote Storage](remote-storage.md) topic for more information on Shared files.
{% endhint %}

Alternativly you can pass in a file name and the byte\[] date you wish to share, our system will then write that information to the user's remote storage, share it and attach that share handle.

```csharp
API.Leaderboards.Client.AttachUGC(board, fileName, data, callback);
```

In this case we are writing a file up to the user's remote storage, if that write or the request to share that file should fail then the callback will contain the result code and a value of true on the bool error.

### Entries

Entries e.g. the records in the board can be queried in several ways.

#### Download Entries

Fetches a series of leaderboard entries for a specified leaderboard. You can ask for more entries than exist, then this will return as many as do exist. The request type indicates how the range should be applied, see [Valve's documentaiton](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardDataRequest) for more information.

```csharp
API.Leaderboards.Client.DownloadEntries(board, request, start, end, callback);
```

Alternatively you can download the entries for a given set of users. This fetches leaderboard entries for an arbitrary set of users on a specified leaderboard. A maximum of 100 users can be downloaded at a time, with only one outstanding call at a time. If a user doesn't have an entry on the specified leaderboard, they won't be included in the result.

```csharp
API.Leaderboards.Client.DownloadEntries(board, users, callback);
```

#### Upload Scores

A user can upload scores and details to a leaderboard at any time. You can control the rules used when uploading scores via the upload method. You can learn more about the upload score method options in [Valve's documentation](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardUploadScoreMethod).

{% hint style="warning" %}
Help, my uploaded score doesn't appear!

or

My uploaded score only appears when I use the Force Update option



The most common cause of this is that you have the sort order on your board backwards from what you intend it to be. Please carefully read the [documentation on the Sort Method option for Leaderboards](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardSortMethod).&#x20;



Also note that once you create a leaderboard with a given sort method it has been observed that it remains with that sort method, and deleting and recreating the board with the same name causes the old sort method to persist. This has to do with how Valve handles the objects in there backend database. The simplest solution is to remove the board, and create a new board with a new name using the proper sorting method.
{% endhint %}

```csharp
API.Leaderboards.Client.UploadScore(board, method, score, details, callback);
```
