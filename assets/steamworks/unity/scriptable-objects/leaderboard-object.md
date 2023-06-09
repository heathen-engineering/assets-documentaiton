# Leaderboard Object

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class LeaderboardObject : ScriptableObject
```

Represents a Steam Leaderboard and is used by the [Steam Settings](steam-settings/) object to initalize the Leaderboard system. This is a wrapper around the [LeaderboardData ](../../data-layer/leaderboard-data.md)object making it a referenceable Unity object.

You create leaderboard objects through thee Steam Settings object by clicking the <mark style="color:green;">+ New</mark> button in the leaderboards list.

![](<../../../../.gitbook/assets/image (184) (1).png>)

From the Steam Settings you can mark the leaderboard as create if missing by ticking the toggle to the left of the name.

![](<../../../../.gitbook/assets/image (152) (1) (1).png>)

![](<../../../../.gitbook/assets/image (165) (1) (1) (1) (1).png>)

You can specify the number of detail entries the board should handle by entering a number in the Details field

{% hint style="warning" %}
Each board can handle up to 64 details and no more than that
{% endhint %}

If your marking your board as Create if Missing e.g. you have ticked the box as indicated above then you should also set the display type and sorting order by selecting the leaderboard in your Steam Settings and editing its values.

![](<../../../../.gitbook/assets/image (153) (1) (1) (1).png>)

{% hint style="danger" %}
None is an available but invalid option for both settings



Why even show it if its invalid, ask Valve, its part of the enums they provide so we expose it.
{% endhint %}

## Events

### User Entry Updated

```csharp
public UnityLeaderboardRankUpdateEvent UserEntryUpdated
```

Invoked when the local user's entry in this board is updated, the handler for this event should take the form of.

```csharp
void HandleEvent(LeaderboardEntry userEntry)
{
    //Do Work
}
```

## Fields and Attributes

### Create If Missing

```csharp
public bool createIfMissing;
```

If true then when the system loads it will search for this board and if not found it will create a new board with settings matching it.

### Sort Method

```csharp
public ELeaderboardSortMethod sortMethod;
```

Defines the [ELeaderboardSortMethod ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardSortMethod)to be used \*\*if\*\* this board is created new

### Display Type

```csharp
public ELeaderboardDisplayType displayType;
```

Defines the [ELeaderboardDisplayType ](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardDisplayType)to be used \*\*if\*\* this board is created new

### API Name

```csharp
public string apiName;
```

The API name of the board

### Display Name

```csharp
public string DisplayName => get;
```

The community display name of the board if any, this is only reinvent for boards created in the Steam Developer Portal and that have been assigned a community name.

### Max Detail Entries

```csharp
public int maxDetailEntries;
```

How many detail entries should be allowed on entries from this board, this is used by quires and doesn't prevent you from adding more or fewer. It is only a hint used by query tools to know how many to watch for.

### Data

```csharp
public LeaderboardData data;
```

The underlying [LeaderboardData](../../data-layer/leaderboard-data.md) object, this is what does all the actual work.

### Valid

```csharp
public bool Valid => get;
```

True if the board's ID is valid, false otherwise.

### Entry Count

```csharp
public int EntryCount => get;
```

Returns the number of records found for this board.

## Methods

### Get User Entry

```csharp
public void GetUserEntry(int maxDetailEntries, Action<LeaderboardEntry, bool> callback)
```

Queries for the local user's entry on this board and invokes the callback when and if found.

* maxDetailEntries\
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../../../../steam/leaderboard-object/).
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
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../../../../steam/leaderboard-object/).
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
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../../../../steam/leaderboard-object/).
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
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../../../../steam/leaderboard-object/).
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
  This indicates how many if any detail entries should be read for each entry on the board. To understand detail entries better please read the article on [Steam Leaderboards](../../../../steam/leaderboard-object/).
* callback\
  A method to be invoked when the process completes

The callback should take the form of

```csharp
void HandleCallback(LeaderboardEntry[] results, bool IOError)
{
    //Do Work
}
```

### Register

```csharp
public void Register();
```

Finds or creates the board according to configuration values. This is handled by the internal system for all boards defined at development time but must be called manually if you define this object at run time.

### Upload Score

```csharp
public void UploadScore(int score, 
                ELeaderboardUploadScoreMethod method, 
                Action<LeaderboardScoreUploaded, bool> callback = null)
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
                Action<LeaderboardScoreUploaded, bool> callback = null)
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
void HandleCallback(LeaderboardScoreUploaded result, bool IOError)
{
    //Do Work
}
```

### ForceUploadScore

Similar to upload score this is a simplified set of upload score commands that assumes you wish to use the "Force Update" method e.g. you want the score to be applied rather or not it is the better value between the current score and the one you are uploading.

```csharp
public void ForceUploadScore(int score)
```

or

```csharp
public void ForceUploadScore(string score)
```

When uploading a string score the system will attempt to parse the score to an int value, this should only be used when your uploading score from a text field and is meant for testing not production use.

### KeepBestUploadScore

Similar to upload score this is a simplified set of upload score commands that assumes you wish to use the "Keep Best" method e.g. you want the best ranking value to be keep rather that is the score you are uploading or the user's current score.

```csharp
public void KeepBestUploadScore(int score)
```

or

```csharp
public void KeepBestUploadScore(string sscore)
```

When uploading a string score the system will attempt to parse the score to an int value, this should only be used when your uploading score from a text field and is meant for testing not production use.

### Attach UGC

```csharp
public void AttachUGC(string fileName, 
        object jsonObject, 
        System.Text.Encoding encoding, 
        Action<LeaderboardUGCSet, bool> callback = null)
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
void HandleCallback(LeaderboardUGCSet result, bool IOError)
{
    //Do Work
}
```
