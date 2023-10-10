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

Steam leaderboards are persistent tables with automatically ordered entries. Leaderboards can be used to display global and friend boards in your game and on your community page. Each title can create up to 10,000 leaderboards, and each leaderboard can be retrieved immediately after a player's score has been uploaded.

There is no limit on the number of players a leaderboard supports. Each leaderboard entry contains a score (as an int) and optionally up to 64 ints of detail data stored as a simple array on the entry. The detailed data can be used to store game-specific information about the play session that resulted in the user's leaderboard entry. This data is not sorted or parsed by Steam and is replaced when a new leaderboard entry is created for the user. Attachments can be linked with the leaderboard via the UGC (User Generated Content) feature of Steam.

Leaderboards can be configured such that only a trusted web API call can set the value. This is strongly recommended if you have any concerns over the validity of leaderboard scores. When the leaderboard's write operation is configured as trusted only a server using the Steam Web API and a publisher token can upload scores to the board. If the board is not configured as a trusted write then anyone can upload any score to the board.

{% hint style="info" %}
Use the Steam Web API to set trusted leaderboard scores

[https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore](https://partner.steamgames.com/doc/webapi/ISteamLeaderboards#SetLeaderboardScore)
{% endhint %}

## Quick Start

First you need to create your achievements on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

### Create

Log into your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="Techincal Tools"><figcaption></figcaption></figure>

From there select the Stats & Achievements > Leaderboards option and create your new boards.&#x20;

Make note of the value you use in the API Name field. You will use it when working with achievements in code.&#x20;

### Publish

You \*\***MUST**\*\* publish your changes in the Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../../../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

### Use

To reference a Leaderboard in your Steam Settings press the "<mark style="color:green;">+ New</mark>" button on the Steam Settings object next to the Leaderboard entry

{% hint style="info" %}
Unfortunately, we cannot import existing leaderboards from Steam directly.



Why?

Valve has not provided an official means to do so through the Steam API.
{% endhint %}

![](<../../../../.gitbook/assets/image (182) (1) (1) (1).png>)

A few key features to know about when you create your Leaderboard.

From the Steam Settings, you can mark the leaderboard as created if missing by ticking the toggle to the left of the name. If ticked, the system will search for the board by name, if it is not found it will create the board for you.

![](<../../../../.gitbook/assets/image (152) (1) (1).png>)

![](<../../../../.gitbook/assets/image (165) (1) (1) (1) (1).png>)

You can also specify the number of `Details` entries the board should handle by entering a number in the Details field

{% hint style="warning" %}
Each board can handle up to 64 details and no more than that
{% endhint %}

Details are a way of storing additional data on a board, you must specify how many the board will hold so that our system can know how many to read from Steam.

If your marking your board as Create if Missing e.g. you have ticked the box as indicated above then you should also set the display type and sorting order by selecting the leaderboard in your Steam Settings and editing its values.

![](<../../../../.gitbook/assets/image (153) (1) (1) (1).png>)

{% hint style="danger" %}
None is an available but invalid option for both settings



Why even show it if it's invalid, ask Valve, it's part of the enums they provide so we expose it.
{% endhint %}

### Details

Understanding the detail array.

A leaderboard is simply a score recorded for a user, Steam will sort these scores according to the sorting method you configured for the board.

In many cases however you need or want additional data linked with that score, rather this is info about the player's build, stats during the session that earned them the score or something else.

You can upload an array of int values along with the player's score, Steam takes up to 64 values e.g. `int[64]` These can be anything you would like as long as they are int and there are less than 64 of them.

To read this data make sure you have set the `Details` field as seen in the inspector for your Leaderboard Object. This tells our system how many details it should read from Steam when reading a user's data. If you leave it at 0 we will not try to read detail values, if you enter a value larger than 64 errors will occur.

The details themselves will be provided in the [LeaderboardEntry ](../../../../heathens-steamworks-complete/unity/objects/leaderboard-entry.md)record returned by leaderboard queries.

### Attachments

Understanding leaderboard attachments.

As with the `Details` You can add additional data to the leaderboard entry in the form of an attachment. This is simply a single file stored in the user's remote storage and linked to the leaderboard entry.

{% hint style="info" %}
Steam copies this item over to the board directly so it will remain even if the user later deletes it from their storage.
{% endhint %}

{% hint style="warning" %}
Because this file is initially uploaded to the remote storage it is subject to the max file size you configured in the app for Steam Cloud aka Steam Remote Storage.
{% endhint %}

Our tools make the process of uploading and attaching files extremely simple. you can use the LeaderboardObject's AttachUGC method to upload and attach any object that is JSON serializable via the Unity JSON utility. e.g.&#x20;

```csharp
leaderboard.AttachUGC("attachmentName", myData, Encoding.UTF8, callback);
```

The above example assumes that `myData` is a JSON serializable object and that callback is a suitable method or delegate with a signature like `void Callback(LeaderbaordUGCSet_t result, bool IOError);` This will create a new file named attachmentName in the user's remote storage and then attach it to the user's entry on this leaderboard.

## Leaderboard Manager

The leaderboard manager is a simple component that greatly simplifies reading and writing data to and from a given leaderboard and exposes helpful events to the Unity Inspector.

![](<../../../../.gitbook/assets/image (181) (1).png>)

You can learn more about the [Leaderboard Manager](../../../../heathens-steamworks-complete/unity/components/leaderboard-manager.md) in its documentation article and by reviewing the [4 Leaderboards](../../../../heathens-steamworks-complete/unity/sample-scenes/leaderboards.md) sample scene.

## How To

### Upload Score

When uploading scores you have several options,&#x20;

{% hint style="info" %}
Upload Method or simply Method

This is a concept you will see in various places when uploading&#x20;
{% endhint %}

#### [Leaderboard Object](../../../../heathens-steamworks-complete/unity/scriptable-objects/leaderboard-object.md)

The most common is to use the LeaderboardObject itself to upload scores. The LeaderboardObject is a ScriptableObject so you can reference it in any script you like and use it as such:

```csharp
leaderboard.UploadScore(42, method, callback);
```

This method requires you to pass in the score, and method of upload and provide a callback in the form of `void Callback(LeaderboardScoreUploaded_t result, bool IOError)` that will be invoked when the process is complete.

{% hint style="info" %}
Callbacks are a common feature of many multi-process systems including Unity itself.  You can [learn more about them here](../../../development/callbacks.md).
{% endhint %}

or

```csharp
leaderboard.UploadScore(42, detailArray, method, callback);
```

This method works the same as the above but can take a detailed array. This would be an array of int values and must not be longer than 64 e.g. `int[64] detailArray` This is commonly used to store additional data about the user's entry.

#### [Leaderboard Manager](../../../../heathens-steamworks-complete/unity/components/leaderboard-manager.md)

You can use the [Leaderboard Manager](../../../../heathens-steamworks-complete/unity/components/leaderboard-manager.md) component;\
This component can be attached to a GameObject to manage a specific leaderboard. It is meant to be used with UI elements or for users who are not comfortable working with Scriptable Objects or the API directly. It serves to simplify the methods and features of the leaderboard system and expose common events to the Unity inspector.

While it's not typical you can interact with the Leaderboard Manager from code such as.

```csharp
leaderboardManager.UploadScore(42);
```

This method takes only a score value and will upload the score with the "Keep Best" upload option.

or

```csharp
leaderboardManager.UploadScore(42, detailArray);
```

This method takes a score and an array of ints, note you can only upload up to 64 ints, to read these ints you must have configured the Details value in the Leaderboard Object on the Steam Settings as shown above.

or

```csharp
leaderboardManager.ForceScore(42);
```

and

```csharp
leaderboardManager.ForceScore(42, detailAray)
```

are available, these do the same as the `UploadScore` version only they do so with the "Force Update" option meaning that even if the score provided is not as good as the current score Steam will still apply it.

#### Leaderboard API

The leaderboard API is what does all the work no matter what method or tool you choose to use. The APIs are all static classes which make no assumptions so you need to provide more information.

```csharp
Leaderboard.API.UploadScore(leaderboard,
                            method,
                            score,
                            detailArray,
                            callback);
```

Because this is a static class we must indicate what leaderboard we want to upload to, this is done by passing in the LeaderboardObject.

Next, we must indicate the upload method; [methods are defined by Steam here](https://partner.steamgames.com/doc/api/ISteamUserStats#ELeaderboardUploadScoreMethod). Typically you would upload with `ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodKeepBest` this will cause the system to keep the best score. You would never upload with `ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodNone` the 3rd option is to Force Update, forcing the board to take whatever you give it; `ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodForceUpdate` this is generally only used to "reset" a board.

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
