# Leaderboard Data

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct LeaderboardData : IEquatable<SteamLeaderboard_t>, 
                                IEquatable<ulong>, 
                                IEquatable<string>
```

A simple struct that provides easy access to a given leaderboard's features and data. The structure is convertible to and from the native and primitive data types for a Steam Leaderboard

```csharp
LeaderboardData fromNative = new SteamLeaderboard_t(123456789);
LeaderboardData fromPrimative = 123456789;
```

Get methods are provided for users that prefer that approach

```csharp
LeaderboardData fromNative = LeaderboardData.Get(new SteamLeaderboard_t(123456789));
LeaderboardData fromPrimative = LeaderboardData.Get(123456789);
```

A Get method with callback can be used to look up the ID and return the resulting board based on its name. This being asynchronous does require the use of a callback;

```csharp
LeaderboardData.Get("boardName", (result, ioError) => {
    if(ioError)
        Debug.Log($"IO Error encountered when searching for boardName");
    else if (result.Valid)
        Debug.Log($"We found the board and its ready to use");
    else
        Debug.Log("No error, but no such board found");
});
```

## Fields and Attributes

### API Name

```csharp
public string apiName;
```

Only set when getting a leaderboard by its name, this is the API name used to look up the leaderboard's ID on the Steam API.

### Id

```csharp
public SteamLeaderboard_t id;
```

The native Steam API ID for this leaderboard. Typically this is found by searching for a board by its name. If you define your boards in the SteamSettings object these will all be found and loaded for you on start up.

### Display Name

```csharp
public string DisplayName => get;
```

Returns the display for the board if the board is valid.

### Valid

```csharp
public bool Valid => get;
```

Returns true if the board ID is valid, this does not insure the ID is correct only that its non-default. If you set an incorrect valid here that is greater than zero this will be true but obviously not a real Leaderboard.

### Entry Count

```csharp
public int EntryCount => get;
```

Returns the total number of entries available for this board

## Methods

### Get User Entry

```csharp
public void GetUserEntry(int maxDetailEntries, Action<LeaderboardEntry, bool> callback)
```

Queries for the local user's entry on this board and invokes the callback when and if found.

* maxDetailEntries\
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../unity/guides/leaderboard-object/).
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardEntry result, bool IOError)
{
    //Do Work
}
```

### Get Top Entries

```csharp
public void GetTopEntries(int count, 
                int maxDetailEntries, 
                Action<LeaderboardEntry[], bool> callback)
```

Queries the leaderboard for the top number of entries.

* count\
  How many top records should be read
* maxDetailEntries\
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../unity/guides/leaderboard-object/).
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardEntry[] results, bool IOError)
{
    //Do Work
}
```

### Get All Entries

```csharp
public void GetAllEntries(int maxDetailEntries, Action<LeaderboardEntry[], bool> callback)
```

Returns all entries on this board

* maxDetailEntries\
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../unity/guides/leaderboard-object/).
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardEntry[] results, bool IOError)
{
    //Do Work
}
```

### Get Entries

```csharp
public void GetEntries(ELeaderboardDataRequest request, 
                int start, 
                int end, 
                int maxDetailEntries, 
                Action<LeaderboardEntry[], bool> callback)
```

* request\
  The type of query you want to run ... See [ELeaderboardDataRequest ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardDataRequest)for details
* start\
  The index to start downloading entries.
* end\
  The index to stop downloading entries.
* maxDetailEntries\
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../unity/guides/leaderboard-object/).
* callback\
  A method to be invoked when the process completes

```csharp
public void GetEntries(UserData[] users, 
                int maxDetailEntries, 
                Action<LeaderboardEntry[], bool> callback)
```

* users\
  The set of users you want to read records for.
* maxDetailEntries\
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../unity/guides/leaderboard-object/).
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardEntry[] results, bool IOError)
{
    //Do Work
}
```

### Get

```csharp
public static void Get(string name, Action<LeaderboardData, bool> callback)
```

An asynchronous look up to get a leaderboard based on its API name

* name\
  The API name of the board to find
* callback\
  a method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardData result, bool IOError)
{
    //Do Work
}
```



```csharp
public static LeaderboardData Get(ulong id)
```

Converts a ulong ID value into a LeaderboardData object

```csharp
public static LeaderboardData Get(SteamLeaderboard_t id)
```

Converts a SteamLeaderboard\_t id into a LeaderboardData object

### Get or Create

```csharp
public static void GetOrCreate(string name, 
                ELeaderboardDisplayType displayType, 
                ELeaderboardSortMethod sortMethod, 
                Action<LeaderboardData, bool> callback)
```

Searches for a board and returns it if found, if not found it will create a board by that name.

* name\
  The API name of the board to find or create
* displayType\
  The [ELeaderboardDisplayType ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardDisplayType)of the board
* sortMethod\
  The [ELeaderboardSortMethod ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardSortMethod)of the board
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardData result, bool IOError)
{
    //Do Work
}
```

### Upload Score

```csharp
public void UploadScore(int score, 
                ELeaderboardUploadScoreMethod method, 
                Action<LeaderboardScoreUploaded_t, bool> callback = null)
```

* score\
  The score to upload
* method\
  The [ELeaderboardUploadScoreMethod ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardUploadScoreMethod)to be used on upload
* callback\
  A method to be invoked when the process completes

```csharp
public void UploadScore(int score, 
                int[] scoreDetails, 
                ELeaderboardUploadScoreMethod method, 
                Action<LeaderboardScoreUploaded_t, bool> callback = null)
```

* score\
  The score to upload
* scoreDetails\
  Additional details to add to the entry if accepted
* method\
  The [ELeaderboardUploadScoreMethod ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardUploadScoreMethod)to be used on upload
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardScoreUploaded_t result, bool IOError)
{
    //Do Work
}
```

### Attach UGC

```csharp
public void AttachUGC(string fileName, 
        object jsonObject, 
        System.Text.Encoding encoding, 
        Action<LeaderboardUGCSet_t, bool> callback = null)
```

* fileName\
  The name of the file to be saved, this is only used when created the file and can be removed or changed later without breaking the entry on the board
* jsonObject\
  Any "Serializable" object, we use Unity's JsonUtility to serialize your object to JSON for writing.
* encoding\
  (optional) the encoding method you want to use, if not provided we will use UTF8
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardUGCSet_t result, bool IOError)
{
    //Do Work
}
```

