---
description: Understanding Steam Leaderboards and the Heathen Engineering tool kit
---

# 🥇 Leaderboards

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% embed url="https://youtu.be/6WQBal2brKI" %}

Steam leaderboards are persistent tables with automatically ordered entries. Leaderboards can be used to display global and friend boards in your game and on your community page. Each title can create up to 10,000 leaderboards, and each leaderboard can be retrieved immediately after a player's score has been uploaded.

There is no limit on the number of players a leaderboard supports. Each leaderboard entry contains a score (as an int) and optionally up to 64 ints of detail data stored as a simple array on the entry. The detailed data can be used to store game-specific information about the play session that resulted in the user's leaderboard entry. This data is not sorted or parsed by Steam and is replaced when a new leaderboard entry is created for the user. Attachments can be linked with the leaderboard via the UGC (User Generated Content) feature of Steam.

Leaderboards can be configured such that only a trusted web API call can set the value. This is strongly recommended if you have any concerns over the validity of leaderboard scores. When the leaderboard's write operation is configured as trusted only a server using the Steam Web API and a publisher token can upload scores to the board. If the board is not configured as a trusted write then anyone can upload any score to the board.

{% hint style="info" %}
Use the Steam Web API to set trusted leaderboard scores

[https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore](https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore)
{% endhint %}

## Quick Start

First, you need to create your achievements on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

Log into your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="Techincal Tools"><figcaption></figcaption></figure>

From there select the Stats & Achievements > Leaderboards option and create your new boards.&#x20;

Make note of the value you use in the API Name field. You will use it when working with achievements in code.&#x20;

### Publish

You \*\***MUST**\*\* publish your changes in the Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../../../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

## Troubleshooting&#x20;

### Upload ignores my value

A common issue when your start is that it may appear that the leaderboard is ignoring the score you upload, or that it only takes scores in the opposite direction you intended.

For example, if you upload 10, then upload 11 it may ignore the 11 but if you upload 9 it will take the 9.

#### Why?

Steam Leaderboards are configured to sort scores in a particular direction and when you upload a score you are typically doing so as "Keep Best".&#x20;

```csharp
board.UploadScore(42,
    ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodKeepBest,
    (result, error) =>
    {
        if(!error)
            Debug.Log("Recorded: " + result.m_nScore +
                      "New Rank: " + result.m_nGlobalRankNew);
    });
```

The "Keep Best" option tells Steam to only record the new value you present \*\* **if** \*\* that value is better than the previous value recorded. This is determined by the "sort order" you configured for the board in the Steam Portal.

### How to Fix?

Assuming you have the board configured incorrectly simply update its configuration in the Steam portal and then publish the changes.

{% hint style="warning" %}
You **MUST ALWAYS** publish changes when making edits in the Steam Portal. It does not apply the moment you make the change in the portal it is a Perforce-based source control system that requires you to publish your changes.
{% endhint %}

If for some reason you find your board still acts like it's sorted the other way around, this is likely due to an issue seen a few times with Steam's backend services. Submit a support case letting Valve know that your board appears bugged and is not changing its sort direction as it should.

To work around the issue make a new board (with a new name) and set it up with the sort of direction you desire; do not delete the broken board … please … so Valve can review it.

## Examples

### Get Leaderboard

{% tabs %}
{% tab title="Toolkit for Unity" %}
Assumes targetBoard is a [LeaderboardObject ](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-object.md)or [LeaderboardData](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-data.md)

## C\#

```csharp
//Leaderboard Object will be "got" for you by the initialization process
//For Leaderboard Data we need as its a struct and not a reference we need
//To get its ID before we can use it

//Before we can use a leaderboard we need to get its ID ... not its API Name ... its ID
//The static function takes in the api name and a delegate to be called when the process is completed
//This is an asynchronous method ... a delegate is simply a pointer to a function
//You could give it a named function you defined in your class but far more commonly you use an anonymous function as we have here
LeaderboardData.Get(apiName, (data, ioError) =>
{
    if (!ioError)
    {
        targetBoard = data;
        Debug.Log($"Found {apiName} with ID {targetBoard.id.m_SteamLeaderboard}");

        //At this point you now have the board and do things with it .... see the functions below that give examples of working with the board such as reading and writing data
    }
    else
    {
        Debug.LogError($"An IO error occurred while attempting to read {apiName}");
    }
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to create a variable to store the CallResult
// This must be maintained until the CallResult is returned and complete
CCallResult<YourClass, LeaderboardFindResult_t> m_LeaderboardFindResult_t;

// Next call FindLeaderboard storing the handle
SteamAPICall_t handle = SteamUserStats()->FindLeaderboard(StringCast<ANSICHAR>(*board).Get());
// Use the handle with the CallResult created earlier
// Provide a pointer a suitable function to be called when the result
// Completes Valve will invoke the function passing the requested data
m_LeaderboardFindResult_t.Set(handle, this, &YourClass::Callback);

// Example Function to be called by the CallResult delegate
// Note that Unreal runs the Callback loop on a background thread
// This means you will need to create a GameThreadTask to bring the 
// Result forwarded to the GameThread
void YourClass::Callback(LeaderboardFindResult_t* Response, bool bIOError)
{
	if (!bIOError)
	{
		int64 boardId = static_cast<int64>(Response->m_hSteamLeaderboard);
		bool found = Response->m_bLeaderboardFound > 0 ? true : false;

		// Execute the delegate on the game thread asynchronously
		FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this, boardId, found]()
		{
			if (Callback.IsBound())
			{
				UE_LOG(LogTemp, Log, TEXT("Board found and callback invoked"));
				Callback.Execute(boardId, found);
			}
			else
			{
				UE_LOG(LogTemp, Log, TEXT("Board found, no callback to invoke"));
			}
		}, TStatId(), nullptr, ENamedThreads::GameThread);
		GameThreadTask->Wait();
	}
	else
	{
		// Execute the delegate on the game thread asynchronously
		FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this]()
		{
			if (Callback.IsBound())
				Callback.Execute(0, false);
		}, TStatId(), nullptr, ENamedThreads::GameThread);
		GameThreadTask->Wait();
	}
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// First create a CallResult of type LeaderboardFindResult_t
// This can be used with both Find and Find or Create
// This must be held in memory until the process is returned
// So you will want to create it as a private variable on some object
// That will not be destroyed.
CallResult<LeaderboardFindResult_t> m_LeaderboardFindResult_t = CallResult<LeaderboardFindResult_t>.Create();

// Call Find or FindOrCreate storing the handle
var handle = SteamUserStats.FindLeaderboard(apiName);
// or
var handle = SteamUserStats.FindOrCreateLeaderboard(apiName, sortMethod, displayType);

// Once you have the handle you can set the CallResult
m_LeaderboardFindResult_t.Set(handle, (results, error) =>
{
    // Handle the result if the error is false
    // You want to store the results.m_hSteamLeaderboard for later use
});
```
{% endtab %}
{% endtabs %}

### Upload Score

{% tabs %}
{% tab title="Toolkit for Unity" %}
Assumes targetBoard is a [LeaderboardObject ](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-object.md)or [LeaderboardData](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-data.md)

There are multiple overloads to Upload Scores to a leaderboard, see the class description for a full list.

## C\#

```csharp
// Call Upload Score passing in any details and indicating an upload Method
// This is an asynchronous function so the last parameter is a delegate
// That will be run when the process completes
targetBoard.UploadScore(score, details, uploadMethod, (callbackResult, ioError) =>
{
    // Handle the result if ioError is false
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to create a variable to store the CallResult
// This must be maintained until the CallResult is returned and complete
CCallResult<YourClass, LeaderboardScoreUploaded_t> m_LeaderboardFindResult_t;

SteamAPICall_t handle = SteamUserStats()->UploadLeaderboardScore(board, method, score, data.GetData(), data.Num());
// Use the handle with the CallResult created earlier
// Provide a pointer a suitable function to be called when the result
// Completes Valve will invoke the function passing the requested data
m_LeaderboardScoreUploaded_t.Set(handle, this, &YourClass::Callback);

// Example Function to be called by the CallResult delegate
// Note that Unreal runs the Callback loop on a background thread
// This means you will need to create a GameThreadTask to bring the 
// Result forwarded to the GameThread
void YourClass::Callback(LeaderboardScoreUploaded_t* Response, bool bIOError)
{
	// Execute the delegate on the game thread asynchronously
	FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this, bIOError, Response]()
	{
		if (!bIOError)
		{
			if (Callback.IsBound())
				Callback.Execute(Response->m_bSuccess == 1, Response->m_bScoreChanged == 1, Response->m_nGlobalRankNew, Response->m_nGlobalRankPrevious);
		}
		else if (Callback.IsBound())
			Callback.Execute(false, false, 0, 0);
	}, TStatId(), nullptr, ENamedThreads::GameThread);
	GameThreadTask->Wait();
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// First create a CallResult of type LeaderboardScoreUploaded_t
// This must be held in memory until the process is returned
// So you will want to create it as a private variable on some object
// That will not be destroyed.
CallResult<LeaderboardScoreUploaded_t> m_LeaderboardScoreUploaded_t = CallResult<LeaderboardScoreUploaded_t>.Create();

// Call upload leaderboard score
var handle = SteamUserStats.UploadLeaderboardScore(boardId, method, score, details, details == null ? 0 : details.Length);

// Once you have the handle you can set the CallResult
m_LeaderboardScoreUploaded_t.Set(handle, (result, error) =>
{
    // Handle the result if the error is false
});
```
{% endtab %}
{% endtabs %}

### Get User's Entry

{% tabs %}
{% tab title="Toolkit for Unity" %}
Assumes targetBoard is a [LeaderboardObject ](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-object.md)or [LeaderboardData](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-data.md)

## C\#

```csharp
targetBoard.GetUserEntry(detailEntriesCount, (foundEntry, ioError) =>
{
    // Handle the found entry if ioError is false
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to create a variable to store the CallResult
// This must be maintained until the CallResult is returned and complete
CCallResult<YourClass, LeaderboardScoresDownloaded_t> m_LeaderboardScoresDownloaded_t;

SteamAPICall_t handle = SteamUserStats()->DownloadLeaderboardEntriesForUsers(leaderboard, targetUsers, numUsers);
// Use the handle with the CallResult created earlier
// Provide a pointer a suitable function to be called when the result
// Completes Valve will invoke the function passing the requested data
m_LeaderboardScoresDownloaded_t.Set(handle, this, &YourClass::Callback);

// Example Function to be called by the CallResult delegate
// Note that Unreal runs the Callback loop on a background thread
// This means you will need to create a GameThreadTask to bring the 
// Result forwarded to the GameThread
void YourClass::Callback(LeaderboardScoresDownloaded_t* Response, bool bIOError)
{
    	// Execute the delegate on the game thread asynchronously
	FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this, bIOError, Response]()
	{
		// Handle the results
	}, TStatId(), nullptr, ENamedThreads::GameThread);
	GameThreadTask->Wait();			
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// First create a CallResult of type LeaderboardScoresDownloaded_t
// This must be held in memory until the process is returned
// So you will want to create it as a private variable on some object
// That will not be destroyed.
CallResult<LeaderboardScoresDownloaded_t> m_LeaderboardScoresDownloaded_t = CallResult<LeaderboardScoresDownloaded_t>.Create()

// Call upload leaderboard score
var handle = SteamUserStats.DownloadLeaderboardEntriesForUsers(boardId, new CSteamID[]{ SteamUser.GetSteamID() }, 1);

// Once you have the handle you can set the CallResult
m_LeaderboardScoresDownloaded_t.Set(handle, (results, error) =>
{
    request.callback.Invoke(ProcessScoresDownloaded(results, error, request.maxDetailsPerEntry), error);
    waiting = false;
});
```
{% endtab %}
{% endtabs %}

### Get Entries

{% tabs %}
{% tab title="Toolkit for Unity" %}
Assumes targetBoard is a [LeaderboardObject ](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-object.md)or [LeaderboardData](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-data.md)

## C\#


{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

## C++
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Attach File

{% tabs %}
{% tab title="Toolkit for Unity" %}
Assumes targetBoard is a [LeaderboardObject ](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-object.md)or [LeaderboardData](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-data.md)

## C\#


{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

## C++
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Get Attached File

{% tabs %}
{% tab title="Toolkit for Unity" %}
Assumes targetBoard is a [LeaderboardObject ](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-object.md)or [LeaderboardData](../../../../toolkit-for-steamworks/unity/classes-and-structs/leaderboard-data.md)

## C\#


{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

## C++
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}
