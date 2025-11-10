# Leaderboards

{% embed url="https://youtu.be/6WQBal2brKI" %}

Steam leaderboards are persistent, automatically sorted tables used to display scores globally or among friends. They can appear both in-game and on your title’s Steam community page. Each game can create up to 10,000 unique leaderboards, and scores are retrievable immediately after upload.

Leaderboards support an unlimited number of players. Each entry stores a required score (as an `int`) and optionally up to 64 `int` values of detail data. This detail data is a simple array used for session-specific context, such as character used, time taken, or other gameplay stats. It’s not parsed or sorted by Steam and is overwritten when a new score is submitted.

You can also associate leaderboard entries with Steam UGC (User-Generated Content), allowing you to link replays, loadouts, or screenshots to scores.

Leaderboards can be configured to accept score submissions only via trusted server-side API calls. This is highly recommended to prevent tampering. When using this setting, only a server with access to the Steam Web API and your publisher token can submit scores. If left untrusted, any client can submit any score, which opens the door to abuse.

{% hint style="info" %}
Use the Steam Web API to set trusted leaderboard scores

[https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore](https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore)
{% endhint %}

## Quick Start

First, you need to create your achievements on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

Log in to your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../.gitbook/assets/image (236).png" alt="Techincal Tools"><figcaption></figcaption></figure>

From there, select the Stats & Achievements > Leaderboards option and create your new boards.&#x20;

Make a note of the value you use in the API Name field. You will use it when working with achievements in code.&#x20;

### Publish

You \*\***MUST**\*\* publish your changes in the Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

## Troubleshooting&#x20;

### Upload ignores my value

A common issue when your start is that it may appear that the leaderboard is ignoring the score you upload, or that it only takes scores in the opposite direction you intended.

For example, if you upload 10, then upload 11, it may ignore the 11, but if you upload 9 it will take the 9.

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

Assuming you have the board configured incorrectly, simply update its configuration in the Steam portal and then publish the changes.

{% hint style="warning" %}
You **MUST ALWAYS** publish changes when making edits in the Steam Portal. It does not apply the moment you make the change in the portal it is a Perforce-based source control system that requires you to publish your changes.
{% endhint %}

If for some reason you find your board still acts like it's sorted the other way around, this is likely due to an issue seen a few times with Steam's backend services. Submit a support case letting Valve know that your board appears to be bugged and is not changing its sort direction as it should.

To work around the issue make a new board (with a new name) and set it up with the sort of direction you desire; do not delete the broken board … please … so Valve can review it.

***

## Advanced Profiles

Rich public user profiles can be significant to social games

<figure><img src="../.gitbook/assets/image (197).png" alt=""><figcaption><p>Example of a Dota2 user profile from a random Google image</p></figcaption></figure>

To be effective, profiles need to be accessible anytime a player’s name is visible. That includes offline friends, leaderboard entries, teammates, or opponents who beat you. The profile must be viewable by any user who sees it, without needing to be friends or share a lobby.

Steam’s rich presence can help in some cases. For example, you might see “Main Menu” under a friend’s name. That comes from rich presence, but it only works for yourself and your friends.

For everything else, the data is stored in a profile object. In DOTA’s case, it’s probably stored directly on the account, since DOTA has access to far more Steam features than most developers. That said, we can get close to the same result by storing profile data using leaderboards.

### What Is This?

The goal is to create a publicly accessible player profile, similar to what you see in games like DOTA. These profiles let players show off in-game achievements, favourite builds, top stats, and more — all viewable by other users even outside of active lobbies or friendships.

Steam Leaderboards are used for this because they’re globally readable and can store more than just a score. They include a `details` array (up to 64 integers) and support a UGC attachment per entry, which together allow for rich, flexible data storage.

### How Does It Work?

Start by deciding what data you want players to display in their profiles, such as favourite character, highest level reached, clan affiliation, or other game-specific highlights.

This information should be stored in a structured format that can be serialized. Then, pack the relevant values into an `int[]` using the leaderboard’s `details` field. Since this is limited to 64 integers, efficient packing is key. For instance, booleans can be stored using bit flags, and enums or IDs are already integer-friendly.

While the `details` array is great for compact, high-speed lookups; more descriptive or extended profile data (like full builds or character layouts) should go in a UGC attachment. This can be a file stored via Steam Remote Storage, serialized into a byte array.

Once set up, this profile data is uploaded to the leaderboard using a standard score submission. You can alternate the score or increment it to signal a new version. After uploading, the UGC file is attached to the leaderboard entry, allowing others to fetch it alongside the entry’s details.

### Why Use Both?

**Leaderboard Details (`int[]`)**: Fast, lightweight, and instantly accessible. Ideal for stats, flags, and IDs.

**Leaderboard Attachment (UGC)**: More flexible and suited to richer or nested data. Use it to store full profile objects as JSON, binary data, or other formats.

Steam retains attachments even if the original file is deleted from remote storage, making it a stable way to associate additional data with leaderboard entries.

### Reading the Profile

To read a user’s profile, query the leaderboard entry using their Steam ID or another identifier. The returned data will include the score, `details`, and the attachment if one exists. You can then deserialize the attachment back into a usable profile structure in your game.

This system enables persistent, shareable profiles that work outside of direct Steam relationships and are visible wherever player names are shown — in leaderboards, match histories, or UI elements.

***

## Examples

### Get Leaderboard

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Declare your leaderboard in your Settings, and we will "get" the board for you on initialisation. This will also mean the leaderboard will be "generated" in the SteamTools.Game.Leaderboards static class makes it accessible to other tools and easier to work with in code.

<figure><img src="../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

It is possible to create leaderboards at runtime if they don't already exist

<figure><img src="../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

or you can do this right on the component script, however, if its not in your settings, it wont be available in your SteamTools.Game.Leaderboards

<figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

## C\#

You do not need to "Get" leaderboards that you defined in your settings and generated a wrapper for. We will get them for you on initialisation before we raise the "Ready" event so you can access them directly.

```csharp
SteamTools.Game.Leaderboards.Feet_Traveled
```

For boards that are not defined in the settings you can still get them or create them in C#

```csharp
// Get a board that was created in Steamworks developer portal previously
LeaderboardData.Get(apiName, (data, ioError) =>
{
    if (!ioError)
    {
        targetBoard = data;
        Debug.Log($"Found {apiName} with ID {targetBoard.id.m_SteamLeaderboard}");

        //At this point, you now have the board and do things with it .... see the functions below that give examples of working with the board such as reading and writing data
    }
    else
    {
        Debug.LogError($"An IO error occurred while attempting to read {apiName}");
    }
});

// Or Get or Create, meaning it will get the existing board if any
// or create the board if none.
LeaderboardData.GetOrCreate(apiName
    , ELeaderboardDisplayType.k_ELeaderboardDisplayTypeNumeric
    , ELeaderboardSortMethod.k_ELeaderboardSortMethodDescending
    , (data, ioError) =>
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

<figure><img src="../.gitbook/assets/image (214).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to create a variable to store the CallResult
// This must be maintained until the CallResult is returned and complete
CCallResult<YourClass, LeaderboardFindResult_t> m_LeaderboardFindResult_t;

// Next call FindLeaderboard storing the handle
SteamAPICall_t handle = SteamUserStats()->FindLeaderboard(StringCast<ANSICHAR>(*board).Get());
// Use the handle with the CallResult created earlier
// Provide a pointer to a suitable function to be called when the result
// Completes Valve will invoke the function, passing the requested data
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
// First, create a CallResult of type LeaderboardFindResult_t
// This can be used with both Find and Find or Create
// This must be held in memory until the process is returned
// So you will want to create it as a private variable on some object
// That will not be destroyed.
CallResult<LeaderboardFindResult_t> m_LeaderboardFindResult_t = CallResult<LeaderboardFindResult_t>.Create();

// Call Find or FindOrCreate, storing the handle
var handle = SteamUserStats.FindLeaderboard(apiName);
// or
var handle = SteamUserStats.FindOrCreateLeaderboard(apiName, sortMethod, displayType);

// Once you have the handle, you can set the CallResult
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
## Code Free

You can use the Leaderboard modular component to work with leaderboards in your game.&#x20;

<figure><img src="../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

Use the drop-down to select which leaderboard you want to work with. You can then add settings:

<figure><img src="../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

then add the Upload settings&#x20;

<figure><img src="../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

These will let you set the score and details and provides you with an easy to use Upload function that can optionally be used to attach a UGC item that can be called from a Unity Action or from code.

<figure><img src="../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

## C\#

You can upload a score in a few ways

```csharp
// Upload a simple score asking Steam to record the score if its better than 
// the current score.
SteamTools.Game.Leaderboards.Feet_Traveled.UploadScoreKeepBest(42);
// do the same but with additional details in the form of an int[]
SteamTools.Game.Leaderboards.Feet_Traveled.UploadScoreKeepBest(42, details);

// Upload a score asking Steam to take it no matter the current score
SteamTools.Game.Leaderboards.Feet_Traveled.UploadScoreForceUpdate(42);
// do the same but with additional details in teh form of an int[]
SteamTools.Game.Leaderboards.Feet_Traveled.UploadScoreForceUpdate(42, details);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to create a variable to store the CallResult
// This must be maintained until the CallResult is returned and complete
CCallResult<YourClass, LeaderboardScoreUploaded_t> m_LeaderboardFindResult_t;

SteamAPICall_t handle = SteamUserStats()->UploadLeaderboardScore(board, method, score, data.GetData(), data.Num());
// Use the handle with the CallResult created earlier
// Provide a pointer to a suitable function to be called when the result
// Completes Valve will invoke the function, passing the requested data
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
## Code Free

You can use the Leaderboard modular component to work with leaderboards in your game.&#x20;

<figure><img src="../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

Use the drop-down to select which leaderboard you want to work with. You can then add fields:

<figure><img src="../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

Then add User Entries

<figure><img src="../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

This exposes a reference to a Leaderboard Entry UI component and adds General Events, which it will use to monitor state change for the user's record.

The Steam Leaderboard Entry UI leverages the [User ](user.md)component, extending it to also display the Score and Rank from a Leaderboard Entry.

{% hint style="success" %}
You don't have to set the "Local User" feature of [User](user.md); the Leaderboard Entry passed in will carry the local user with it.
{% endhint %}

<figure><img src="../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
SteamTools.Game.Leaderboards.Feet_Traveled.GetUserEntry(detailEntriesCount, (foundEntry, ioError) =>
{
    // Handle the found entry if ioError is false
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

We have a Task

<figure><img src="../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

And classic callback style options

<figure><img src="../.gitbook/assets/image (206).png" alt=""><figcaption></figcaption></figure>

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
    //Handle the results as you see fit
});
```
{% endtab %}
{% endtabs %}

### Get Entries

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Leaderboard modular component to work with leaderboards in your game.&#x20;

<figure><img src="../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

Use the drop-down to select which leaderboard you want to work with. You can then add settings:

<figure><img src="../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

This gives you fields that can be used to define your display list, it works by spawning an instance of the "Entry Template" for each record found.

<figure><img src="../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

The Entry Template is a Leaderboard Entry UI component which works with the [User](user.md) component to display data about the user and record in question.

<figure><img src="../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

You can now use the Leaderbord object to get records and display them automatically.

<figure><img src="../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
//You have several quality-of-life shortcuts to reading records in different ways
//In all cases, the final parameter is a delegate that will be called when the
//process completes and will contain the results found if any.

//Top X number of records
int howMany = 42;
int detailsCount = 0;
SteamTools.Game.Leaderboards.Feet_Traveled.GetTopEntries(howMany, 
    detailsCount, 
    (entriesFound, ioError) =>
    {
        //Handle the entries found if ioError is false
    });

//Get entries for specific users
UserData[] users; //set this to who you want to read for
int detailsCount = 0;
SteamTools.Game.Leaderboards.Feet_Traveled.GetEntries(users, 
    detailsCount, 
    (entriesFound, ioError) =>
    {
        //Handle the entries found if ioError is false
    });

//Get entries around the user's entry (includes the user's entry)
int beforeUser = -5;
int afterUser = 5;
int detailsCount = 0;
SteamTools.Game.Leaderboards.Feet_Traveled.GetEntries(ELeaderboardDataRequest.k_ELeaderboardDataRequestGlobalAroundUser, 
    beforeUser, 
    afterUser, 
    detailsCount, 
    (entriesFound, ioError) =>
    {
        //Handle the entries found if ioError is false
    });
    
//Get all your friends' entries
int detailsCount = 0;
SteamTools.Game.Leaderboards.Feet_Traveled.GetEntries(ELeaderboardDataRequest.k_ELeaderboardDataRequestFriends, 
    0, 
    0, 
    detailsCount, 
    (entriesFound, ioError) =>
    {
        //Handle the entries found if ioError is false
    });
    
//Get all entries ... really not recommended but it exists
int detailsCount = 0;
SteamTools.Game.Leaderboards.Feet_Traveled.GetAllEntries(detailsCount, 
    (entriesFound, ioError =>
    {
        //Handle the entries found if ioError is false
    });
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

We have both Tasks

<figure><img src="../.gitbook/assets/image (207).png" alt=""><figcaption></figcaption></figure>

And classic Callback style options

<figure><img src="../.gitbook/assets/image (208).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to create a variable to store the CallResult
// This must be maintained until the CallResult is returned and complete
CCallResult<YourClass, LeaderboardScoresDownloaded_t> m_LeaderboardScoresDownloaded_t;

//Next make the call ... either to "for users"
SteamAPICall_t handle = SteamUserStats()->DownloadLeaderboardEntriesForUsers(leaderboard, targetUsers, numUsers);
// or not
SteamAPICall_t handle = SteamUserStats()->DownloadLeaderboardEntries(leaderboard, dRequest, start, end);
//Both use the same CallResult type so this is the only difference

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

//Next we need to set a "start" and "end"
//Exactly what these do depends on the request type
//It is generally self-explanatory, for example, if you want 
//To get the top 10 results then you want to start at 0 and end at 10

// Call upload leaderboard score
var handle = SteamUserStats.DownloadLeaderboardEntries(boardId, 
                ELeaderboardDataRequest.k_ELeaderboardDataRequestGlobal, //type
                0 // Start
                10 //End
                );

// Once you have the handle you can set the CallResult
m_LeaderboardScoresDownloaded_t.Set(handle, (results, error) =>
{
    //Handle the results as you see fit
});
```
{% endtab %}
{% endtabs %}

### Attach File

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Follow the instructions on the Upload Score example and use the Upload(T attachment) funciton to upload a score and attach a file at the same time. You will need to call Upload(T attachment) in C#.

## C\#

```csharp
//The SteamLeaderboardUpload component will use "attachment" as the
//temporary file name, it is safe to overwrite/clear this after upload once 
//the file is attached.
//Note fileData can be an object of any type as long as it is [Serializable]
leaderboardUpload.Upload(fileData);

//Note the file will need a name but this is just the name of the file for the temporary upload
//So this is the name that will be in the user's Remote Storage, once attached we can remove it to save space.
//we like to us the same name all the time "tempFile" and we do not bother removing it instead we just let it 
//overwrite each time as a means to hold the space for future attachments
SteamTools.Game.Leaderboards.Feet_Traveled.AttachUGC("tempFile", fileData, (ugcResult, ugcIoError) =>
{
    if (!ugcIoError)
    {
        if (ugcResult.Result == Steamworks.EResult.k_EResultOK)
            Debug.Log($"Attached file data to user entry on board {apiName}");
        else
            Debug.LogError($"Failed to attach file data to user entry on board {apiName}, Response Result = {ugcResult.Result}");
    }
    else
    {
        Debug.LogError($"Failed to attach file data to user entry on board {apiName}, IO Error!");
    }
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

This is a 3-step process

### Upload data to attach

You can use Remote Storage Write or Write Async to do this

<figure><img src="../.gitbook/assets/image (209).png" alt=""><figcaption></figcaption></figure>

### Mark the newly created file as "shared"&#x20;

<figure><img src="../.gitbook/assets/image (210).png" alt=""><figcaption></figcaption></figure>

### Attach the resulting Ugc Handle to the board

<figure><img src="../.gitbook/assets/image (211).png" alt=""><figcaption></figcaption></figure>

## C++

As with the blueprints, this will require 3 steps, each is asynchronous&#x20;

```cpp
// First, we need to create our 3 CallResult entries
// File Write ASync Complete
CCallResult<YourClass, RemoteStorageFileWriteAsyncComplete_t> m_RemoteStorageFileWriteAsyncComplete_t;
// File Share Complete
CCallResult<YourClass, RemoteStorageFileShareResult_t> m_RemoteStorageFileShareResult_t;

// Next, we need to upload our file data
// Assuming
FString name; // The file name
TArray<uint8> data; // The data to upload

// Then we call the FileWriteAsync
SteamAPICall_t handle = SteamRemoteStorage()->FileWriteAsync(StringCast<ANSICHAR>(*name).Get(), data.GetData(), data.Num());
// And set the handle
m_RemoteStorageFileWriteAsyncComplete_t.Set(handle, this, &YouClass::WriteComplete);

// In your WriteComplete function
// This uses the same file name as before
void YouClass::WriteComplete(RemoteStorageFileWriteAsyncComplete_t* result, bool ioError)
{
    // Share the new file
    SteamAPICall_t handle = SteamRemoteStorage()->FileShare(StringCast<ANSICHAR>(*name).Get());
    m_RemoteStorageFileShareResult_t.Set(handle, this, &YourClass::ShareComplete);
}

// This requires you to know the Board ID you want to attach the file to
// This is the same ID you got when you "found" or "created" the board
// Now in your ShareComplete funciton
void YourClass::ShareComplete(RemoteStorageFileShareResult_t* result, bool ioError)
{
    // Attach the share handle to the target board
    SteamAPICall_t handle = SteamUserStats()->AttachLeaderboardUGC(boardId, result->m_hFile);
    m_LeaderboardUGCSet_t.Set(handle, this, &YourClass::AttachComplete);
}

void YourClass::AttachComplete(LeaderboardUGCSet_t* result, bool ioError)
{
    // The process is now complete
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// First create your CallResult to catch the results we will need

// This call result is invoked when file write to remote storage is complete
CallResult<RemoteStorageFileWriteAsyncComplete_t> m_RemoteStorageFileWriteAsyncComplete_t = CallResult<RemoteStorageFileWriteAsyncComplete_t>.Create()

// This call result is invoked when the file is shared and we have a share ID
CallResult<RemoteStorageFileShareResult_t> m_RemoteStorageFileShareResult_t = CallResult<RemoteStorageFileShareResult_t>.Create();

// This call result is invoked when the shared file ID is attached to the board
CallResult<LeaderboardUGCSet_t> m_LeaderboardUGCSet_t = CallResult<LeaderboardUGCSet_t>.Create();

// Assuming 
string file; // the name of the file to write
byte[] data; // the data to write to the file

// Call FileWriteAsync
var handle = SteamRemoteStorage.FileWriteAsync(file, data, (uint)data.Length);
// And set the handle to a valid delegate
m_RemoteStorageFileWriteAsyncComplete_t.Set(handle, WriteComplete);


// In the WriteCompleteis where we will "share" the file
void WriteComplete(RemoteStorageFileWriteAsyncComplete_t result, bool ioError)
{
    handle = SteamRemoteStorage.FileShare(file);
    m_RemoteStorageFileShareResult_t.Set(handle, ShareCompelte);
}

// Now in the ShareComplete we can attach the shared ID to the board
void ShareComplete(RemoteStorageFileShareResult_t result, bool ioError)
{
    var handle = SteamUserStats.AttachLeaderboardUGC(boardId, result.m_hFile);
    m_LeaderboardUGCSet_t.Set(handle, (r, e) =>
    {
        // Work is done, the data is now uploaded, shared and attached to the board
    });
}
```
{% endtab %}
{% endtabs %}

### Get Attached File

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not Applicable

## C\#

This assumes you already have a LeaderboardEntry you want to read the attachment for. and it assumes the data you are reading is serialized from a serializable object named "SomeObject"

<pre class="language-csharp"><code class="lang-csharp">// Assuming
LeaderboardEntry entry;
<strong>
</strong><strong>entry.GetAttachedUgc&#x3C;ExampleSerializableDataForAttachment>((dataFound, ioError) =>
</strong>{
    if(!ioError)
    {
        //Data Found is your attachment, if any. It is up to you to check and see if that is a default value or actually set data
        //how you do that depends on what kind of object it is ... for a struct you should always implement the IEquitable, IComparable and overloads for == and != operators
    }
});
</code></pre>
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

You will need the UGC Handle for the entry you want to read ... you can get this from the results of a Download Leaderboard Entries

<figure><img src="../.gitbook/assets/image (212).png" alt=""><figcaption></figcaption></figure>

With that, you can then download and read the data

<figure><img src="../.gitbook/assets/image (213).png" alt=""><figcaption></figcaption></figure>

## C++

```csharp
// Create a CallResult for the RemoteStorageDownloadUGCResult_t
CCallResult<YourClass, RemoteStorageDownloadUGCResult_t> m_RemoteStorageDownloadUGCResult_t;

// This assumes you have the leaderboard entry you want to read an 
// attachment for ... you can see how to get a leaderboard entry
// from the Get Entries example above

// So this assumes
LeaderboardEntry_t entry; // from the Get Entries
// We will be using the UgcHandle from the entry
UgcHandle_t ugcHandle = entry.m_hUGC;

// Start the download
SteamAPICall_t handle = SteamRemoteStorage()->UGCDownload(ugcHandle, 0);
m_RemoteStorageDownloadUGCResult_t.Set(handle, this, &YourClass::DownloadComplete);

// Now in your download complete
void YourClass::DownloadComplete(RemoteStorageDownloadUGCResult_t* result, bool ioError)
{
    // We can use the same handle and get the data from this file
    TArray<uint8> fileData;
    fileData.SetNumUninitialized(result->m_nSizeInBytes);
    //This will populate the fileData with the data read
    int dataRead = SteamRemoteStorage()->UGCRead(ugcHandle, fileData.GetData(), result->m_nSizeInBytes, 0, EUGCReadAction::k_EUGCRead_ContinueReadingUntilFinished);
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// This assumes you have the leaderboard entry you want to read an 
// attachment for ... you can see how to get a leaderboard entry
// from the Get Entries example above

// So this assumes
LeaderboardEntry_t entry;
// We will be using the UgcHandle from the entry
UgcHandle_t ugcHandle = entry.m_hUGC;

// Next we need to download this UGC Handle
// To do that we will need to use a CallResult

// This is invoked when the download is completed
CallResult<RemoteStorageDownloadUGCResult_t> m_RemoteStorageDownloadUGCResult_t = CallResult<RemoteStorageDownloadUGCResult_t>.Create();

// Once we have this declared we can set it such as
var handle = SteamRemoteStorage.UGCDownload(ugcHandle , priority);
m_RemoteStorageDownloadUGCResult_t.Set(callbackHandle, DownloadComplete);

// Now in your DownloadComplete handler, you can read the byte[] data of that file
void DownloadComplete(RemoteStorageDownloadUGCResult_t result, bool ioError)
{
    // We call first with empty buffers to get the size of the file
    SteamRemoteStorage.GetUGCDetails(ugcHandle, out _, out _, out int size, out _);
    // We use that size to create a proper buffer
    var results = new byte[size];
    // Now we call again with a properly allocated buffer
    SteamRemoteStorage.UGCRead(handle, results, size, 0, EUGCReadAction.k_EUGCRead_ContinueReadingUntilFinished);
    
    // results is not a byte[] containing the file data
}
```
{% endtab %}
{% endtabs %}
