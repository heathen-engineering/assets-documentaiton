# Leaderboards

## Introduction

```csharp
public static class API.Leaderboards
```

The whole of the leaderboard system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Leaderboard.Client
```

To work with leaderboards from the point of view of a server you should use the Steam Web API for leaderboards.

{% embed url="https://partner.steamgames.com/doc/webapi/ISteamLeaderboards" %}

For more info on how to use the Steamworks Web API please see the [Web API Overview](https://partner.steamgames.com/doc/webapi\_overview).

### What can it do?

Leaderboards are ranked lists of players where a player's score determins there position on the leaderboard. Leaderboards can contain additional data for each entry either as a details array or as an attachment, attachments are useful for playbacks and other large bits of information while details are useful for character builds, player settings, etc.

## How To

{% hint style="success" %}
The [Leaderboard ](../objects/leaderboard.md)object provides simplified access to many of the features found here in. Be sure to read the documentiaton for the [Leaderboard ](../objects/leaderboard.md)object to understand what options are available to you.
{% endhint %}

### Add an attachment

You can attach files to a user's leaderboard entry using the `AttachLeaderboardUGC` option.&#x20;

{% hint style="info" %}
It is typically easier to add attaches to the local user's entry from teh board its self, that is to use the AttachUGC methods availabel on the [Leaderboard](../objects/leaderboard.md) object.
{% endhint %}

Attaches a piece of user generated content the current user's entry on a leaderboard.

This content could be a replay of the user achieving the score or a ghost to race against.

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

{% hint style="info" %}
It is typically easier to get and upload entries from the board its self, that is to use the GetEntries and Upload methods available on the [Leaderboard ](../objects/leaderboard.md)object.
{% endhint %}

#### Download Entries

Fetches a series of leaderboard entries for a specified leaderboard. You can ask for more entries than exist, then this will return as many as do exist. The request type indicates how the range should be applied, see [Valve's documentaiton](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardDataRequest) for more informaiton.

```csharp
API.Leaderboards.Client.DownloadEntries(board, request, start, end, callback);
```

Alternativly you can download the entries for a given set of users. This fetches leaderboard entries for an arbitrary set of users on a specified leaderboard. A maximum of 100 users can be downloaded at a time, with only one outstanding call at a time. If a user doesn't have an entry on the specified leaderboard, they won't be included in the result.

```csharp
API.Leaderboards.Client.DownloadEntries(board, users, callback);
```

#### Upload Scores

A user can upload scores and details to a leaderboard at any time. You can control the rules used when uploading scores via the upload method. You can learn more about the upload score method options in [Valve's documentation](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardUploadScoreMethod).

{% hint style="warning" %}
Help, my uploaded score doesn't appear!

or

My uploaded score only appears when I use the Force Update option



The most common cause of this is that you have the sort order on your board backwards frrom what you intend it to be. Please carfully read the [documentation on the Sort Method option for Leaderboards](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardSortMethod).&#x20;



Also note that once you create a leaderboard with a given sort method it has been observed that it remains with that sort method, and deleting and recreating the board with the same name causes the old sort method to persist. This has to do with how Valve handles the objects in there backend database. The simplest solution is to remove the board, and create a new board with a new name using the proper sorting method.
{% endhint %}

```csharp
API.Leaderboards.Client.UploadScore(board, method, score, details, callback);
```
