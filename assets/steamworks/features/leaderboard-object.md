---
description: Understanding Steam Leaderboards and the Heathen Engineering tool kit
---

# Leaderboards

Leaderboard objects are created on the [`SteamSettings`](steam-settings.md#leaderboard-object) object. To learn more please read the documentation on [Steam Settings](steam-settings.md#leaderboard-object).

{% hint style="info" %}
Steam leaderboard objects can be used to upload score values to the Steam Backend to order users in a ranked list. You can read more about the Steam Leaderboard system here [https://partner.steamgames.com/doc/features/leaderboards](https://partner.steamgames.com/doc/features/leaderboards)
{% endhint %}

## Introduction

Steam leaderboards are persistent tables with automatically ordered entries. Leaderboards can be used to display global and friend boards in your game and on your community page. Each title can create up to 10,000 leaderboards, and each leaderboard can be retrieved immediately after a player's score has been uploaded.

There is no limit on the number of players a leaderboard supports. Each leaderbaord entry contains a score (as an int) and optionally up to 64 ints of detail data stored as a simple array on the entry. The detail data can be used to store game specific information about the play session that resulted in the user's leaderboard entry. This data is not sorted or parsed by Steam, and is replaced when a new leaderboard entry is created for the user. Attachments can be linked with the leaderboard via the UGC (User Generated Content) feature of Steam.

Leaderboards can be configured such that only a trusted web API call can set the value ... this is strongly recomended if you have any concern over the validity of leaderboard scores. When the leaderboard's write operation is configured as trusted only a server using the Steam Web API and a publisher token can upload scores to the board. If the board is not configured as trusted write then anyone can upload any score to the board.

{% hint style="info" %}
Use the Steam Web API to set trusted leaderboard scores

[https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore](https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore)
{% endhint %}

## Leaderboard Object

This is a scriptable object used to define the leaderboard in Unity and used within Unity to query the board and access its informaiton.

### Create

To create a Leaderboard Object press the "+ New" button on the Steam Settings object next to the Leaderboards entry

![](<../../../.gitbook/assets/image (139).png>)

### Configuration

![](<../../../.gitbook/assets/image (140).png>)

#### Name

The name of the board is entered into the first text box on the leaderboard entry and should be the same as the name entered in the Steam Portal.

![](<../../../.gitbook/assets/image (142).png>)

{% hint style="info" %}
You can create leaderboards at run time by creating a board here that does not exist in Steam Portal. To do so select the board in the Project folder and toggle the Create If Missing value.

This will cause the system to search for the board and if its not foudn to create it at run time.
{% endhint %}

![](<../../../.gitbook/assets/image (141).png>)

#### Details

This field is the second text box you will see in the Steam Settings inspector for a leaderboard and represents the number of detail entries you with the board to store. Details is an integer array stored on entry for each user on the board. You can store up to 64 details e.g. int\[64].

{% hint style="danger" %}
You can only store 64 detail entries on a leaderboard entry. If you need more data than that you should use attachments.
{% endhint %}

#### Create If Missing

This field is displayed on the Leaderboard Inspector, to see this inspector you must select the leaderbaord in your project folder as shown in the screen shot above.

If true the system will create the leaderboard if it is missing, meaning it will create a new leaderboard on Steam's backend if no board is found with this name. When this is the case the following 2 fields are important

#### Sort Method

Only used if Create If Missing is true, this determins in what order values should be sorted e.g. is a lower score a higher rank or is a higher score a higher rank. This is the most common thing to get wrong when creating a leaderboard&#x20;

* Sort Method Ascending\
  This means that the highest "ranked" score is the lowest number that is as you look down the leaderboard from rank 1 to rank 100 the values "ascend" e.g. go up.
* Sort Method Descending\
  This means the highest "ranked" score is the higehst number that is as you look down the leaderboard from rank 1 to rank 100 the values "descend" e.g. go down.

#### Display Type

Only used if Create If Missing is true, this determins how a board score should be displayed and used.

* Type Numeric\
  Simple numeric score
* Type Time Seconds\
  The score is a time measured in seconds
* Type Milliseconds\
  The score is a time measured in milliseconds

#### Leaderboard Id

This is populated by the system when the board is located or created. This is a nullable value and can only be accessed from code e.g.

```csharp
if ( board.leaderboardId.HasValue )
    Debug.Log("Board is located and ready for use");
else
    Debug.Log("Board is unknown and cannot be used yet");
```

#### User Entry

This field is not displayed to the inspector but can be accessed from code via&#x20;

```csharp
board.userEntry
```

Every board tracks the local user's current entry and updates this entry when new scores are uploaded as well as when the board is first initalized. The User Entry is of type `ExtendedLeaderboardEntry` as explained below.

#### Evt Board Found

This is a Unity Event which is invoked when the board is first located or created.

#### Evt Query Results

This is a Unity Event that is raised when new results are returned. The paramiter will include details about the query including the results them selves.

#### Evt User Rank Loaded

This is a Unity Event that is raised when the local user's score is updated.

#### Evt User Rank Changed

This is a Unity Event that is raised when the local user's rank is updated, note score can change without changing the user's rank, rank is the position on the board not the specific score.

#### Evt User New High Rank

This is a Unity Event that is raised when the local user achieves a new higher rank value than previously known.

## Extended Leaderboard Entry

This is a custom structure created by Heathen to handle leaderboard entry data. It contains all of the informaiton for a given leaderboard entry and provides easy access to details and attachements. This is the data type used for `LeaderboardObject.userEntry` .

### Fields

#### Entry

This is the `LeaderboardEntry_t` identifying the entry as used by the Steam API.

#### Details

This is the `int[]` used to store the details found on the record.

{% hint style="info" %}
You can access the details in 2 ways

```csharp
var detailValue = record.details[0];
```

or

```csharp
var detailvalue = record[0];
```
{% endhint %}

{% hint style="warning" %}
This will only be populated if you entered a non-zero value in the Details field of the inspector as noted above.
{% endhint %}

#### Rank

The global rank assoceated with this entry. This is the same as reading `entry.m_nGlobalRank`

#### Score

The score assoceated with this entry. This is the same as reading `entry.m_nScore`

#### Ugc Handle

{% hint style="info" %}
UGC stands for User Generated Content and is a system provided by Valve to store various bits of user generated information. It is the same system that handles Steam Workshop, Walkthroughs, Screenshots and most other forms of user generated content.
{% endhint %}

This is the UGC attachment handle assoceated with the entry. This is the same as reading `entry.m_hUGC`

#### Has Changed Ugc File Name

Returns true if the Cashed Ugc File Name is not empty or null

#### Cashed Ugc File Name

Returns the name of the UGC file if any and if loaded.

#### Evt Ugc Downloaded

This is a Unity Event that is raised when the UGC is downloaded

## Use Cases

### Read the user's score (Client)

The local player's score is always available from the moment the board is initalized from the Steam API. From any given leaderboard you can access the `userEntry` which contains all the data about the user's score/rank on that board if any.

```csharp
//Assume leaderboard is a reference to the desired LeaderboardObject
if(leaderboard.userEntry != null)
{
    //The user has an entry in this board
    Debug.Log("The user's rank is: " + leaderboard.userEntry.Rank.ToString());
    Debug.Log("The user's score is: " + leaderboard.userEntry.Score.ToString());
}
```

### Upload a user's score (Client)

{% hint style="warning" %}
Note that only leaderboards that are set to allow "Write" from client can be set from the Client API. If set to trusted, the board can only be set by the Web API with a publisher key.
{% endhint %}

To set the player's score where the system is instructed to only keep the score if it is an improvement for the player.

```csharp
leaderboard.UploadScore(42, 
    ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodKeepBest);
```

To force the score to a particular value.

```csharp
leaderboard.UploadScore(42, 
    ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodForceUpdate);
```

Set the score (keep best) and attach additional data as an int\[]

### Upload score and details (Client)

{% hint style="info" %}
Note you need to indicate how many details will be stored, so that the query system can know how big of a buffer to use when reading scores from the API.
{% endhint %}

{% hint style="danger" %}
A leaderboard can only support 64 ints worth of detail data. If you need to attach more data you should use the [UGC Attachment](leaderboard-object.md#attach-a-file-to-the-users-entry-client) method.
{% endhint %}

![Note the details in this example are set to 0 and will not read any on query](<../../../.gitbook/assets/image (25).png>)

To upload a score with details simply pass the detail array in withe the UploadScore call as shown below.

```csharp
//details is an array of ints, we can pack data into this arrach 
//and store it with the player's score
int[] additionalData = { level, class, etc };
leaderboard.UploadScore(42, 
   additionalData,
   ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodKeepBest);
```

### Attach a file to the user's entry (Client)

Attach additional data to the user's entry via the UGC system. This assumes you have a serializable object that contains the desired data. We will serialize this object to JSON and write that as a file.

```csharp
//This is just an example, you can use any serializable class or struct
[Serializable]
public struct AttachmentData
{
  public string someData;
  public bool someMoreData;
  public List<int> loadsMoreData;
}
```

Then assuming your extra data is in an object such as

```csharp
AttachmentData attachmentData = new attachmentData()
{
   someData = "Hello World",
   someMoreData = true,
   loadsMoreData = { 1, 2, 4, 8, 16, 32, 64 }
};
```

Then we can call

```csharp
leaderboard.AttachLeaderboardUGC("attachmentName",
                                 attachmentData);
```

### Query records from a board (client)

To get entries from the board you need to listen to the `evtQueryResults` event.

```csharp
leaderboard.evtQueryResults.AddListener(HandleQueryResults);
```

Now the HandleQueryResults method will get called when Valve returns results for this board. The method should look something like this.

```csharp
private void HandleQueryResults(LeaderboardScoresDownloaded results)
{
  if(results.bIOFailure)
    Debug.Log("Something went wrong on Valve's side.");
  else
  {
    if(results.playerIncluded)
      Debug.Log("The player has an entry included in this data");
    
    foreach(var result in results.scoreData)
    {
      //result is of type ExtendedLeaderboardEntry
      //result.entry.m_steamIDUser is a CSteamID of the user who this entry is for
      Debug.Log("User Id: " + result.entry.m_steamIDUser);
      Debug.Log("Rank: " + result.Rank);
      Debug.Log("Score: " + result.Score);
      if(result.entry.details != null)
       Debug.Log("The entry has " + result.entry.details.length + " details");
    }
  }
}
```

You can query the results with the QueryEntries method. Note there are several versions of this method to help you perform common queries easily.

```csharp
//Get the top 10
leaderboard.QueryTopEntries(10);

//Get the 10 entries around the player (5 above and below if possible)
leaderboard.QueryPeerEntries(10);
```

&#x20;The UGC attachment can be had from the ExtendedLeaderboardEntry object by calling the `GetAttachedUgc` method

```csharp
if(result.UgcHandle != UGCHandle_t.Invalid)
{
  result.GetAttachedUgc<AttachmentData>((result, hasError) =>
 {
      if(!hasError)
      {        
        //result is of data tyep AttachmentData as we used in examples above.
        Debug.Log(result.someData);
      }
 });
}
```

### React to "New High Score" (Client)

The leaderboard system provides a range of Unity Events for you to work with that can notify your other game systems about key occurrences, such as the local user earning a new high rank. You can work with these events by either registering an event handler through the `Steamworks Behaviour` or by using scripts to register handlers on a specific board.

{% hint style="info" %}
Leaderboard Events notify the listener of which board and which entry had the event.
{% endhint %}

#### Using the Steamworks Behavior

![Screen shot of a Steamworks Behaviour inspector in the Unity Editor](<../../../.gitbook/assets/image (18).png>)

The provided events can be used in the inspector just as you would, for example, a "Click" event on a `UnityEngine.UI.Button` object.

Alternatively you can register this event in code on a specific leaderboard such as

```csharp
myBoard.evtUserNewHighRank.AddListener(HandleNewHighRank);
```

In either case you will need to create a "handler". This is simply a method designed to work with this particular type of event. In the case of evtUserNewHighRank that would be a method which takes as an input a `LeaderboardRankChangeData` object.

```csharp
private void HandleNewHighRank(LeaderboardRankChangeData data)
{
    //DO WORK
}
```

The `LeaderboardRankChangeData` object contains the leaderboard id, name and the users new and old entry.
