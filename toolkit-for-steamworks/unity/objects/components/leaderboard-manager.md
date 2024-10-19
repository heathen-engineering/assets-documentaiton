---
description: The leader in board 👍
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Leaderboard Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

Meant to be added to a game object at or near your leaderboard UI, this behaviour can help you display leaderboard entries and simplifies the process of uploading scores to a leaderboard.

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class LeaderboardManager : MonoBehaviour
```

## Events

### evtUserEntryUpdated

Occurs when the local user's last known user entry is updated. This can only be raised by operations ran from within the Leaderboard Manager ... for example if you call the RefreshUserEntry or GetUserEntries. Then it is likely to be raised assuming the local user has an entry however if you manually query the board using API.Leaderboards or other methods it will not be raised.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LeaderboardEntry arg0)
{
}
```

Then you would register the event such as:\
Assuming `leaderboardManager` is reference to your Leaderboard Manager.

```csharp
leaderboardManager.evtUserEntryUpdated.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    leaderboardManager.evtUserEntryUpdated.RemoveListener(HandleEvent);
}
```

### evtQueryCompleted

Occurs when a query for records complets and contains the results of that query.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LeaderboardEntry[] arg0)
{
}
```

Then you would register the event such as:\
Assuming `leaderboardManager` is reference to your Leaderboard Manager.

```csharp
leaderboardManager.evtQueryCompleted.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    leaderboardManager.evtQueryCompleted.RemoveListener(HandleEvent);
}
```

### evtQueryError

Occurs when a query fails with an error, errors are not generally specified rather it is up to you to check for logical causes such as the leaderboard being null or not being valid.

You would add a listener on this event such as:\
Assuming `leaderboardManager` is reference to your Leaderboard Manager.

Assuming a handler in the form of

```csharp
private void HandleEvent()
{
}
```

Then you would register the event such as:

```csharp
leaderboardManager.evtQueryError.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    leaderboardManager.evtQueryError.RemoveListener(HandleEvent);
}
```

### evtUploadError

Occurs when an attempt to upload scores fails. As with query errors the API doesn't usually provide any additional information. The typical causes are an invalid board or a board that can only be set by the Web API.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent()
{
}
```

Then you would register the event such as:\
Assuming `leaderboardManager` is reference to your Leaderboard Manager.

```csharp
leaderboardManager.evtUploadError.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behaviour using it is destroyed

```csharp
void OnDestroy()
{
    leaderboardManager.evtUploadError.RemoveListener(HandleEvent);
}
```

## Fields and Attributes

### leaderboard

```csharp
public LeaderboardObject leaderboard
```

![](<../../../../.gitbook/assets/image (152) (1).png>)

Set this to the leaderboard you want this manager to "manage"

### LastKnownUserEntry

```csharp
public LeaderboardEntry LastKnownUserEntry => get;
```

The entry for the local user if known, this will be updated any time you recieve informartion from Steam as to the user's current rank/score.

## Methods

### Refresh User Entry

```csharp
public void RefreshUserEntry();
```

Queries the board for the local user's entry.

### Get Top Entries

```csharp
public void GetTopEntries(int count);
```

Queries the board for the top X number of entries.

### Get Near by Entries

```csharp
public void GetNearbyEntries(int beforeUser, int afterUser);
```

Queries the board for entries around the player, before is the number entries before the player's entry and after is the number after the user's entry.

{% hint style="info" %}
Both values should be entered as positive whole numbers.
{% endhint %}

### Get All Friends entries

```csharp
public void GetAllFriendsEntries();
```

This will return all entries for all friends that have an entry in this board.

### Get User Entries

```csharp
public void GetUserEntries(IEnumerable<UserData> users);
```

This will return entries for each of the indicated user's if they have an entry to return.

### Upload Score

```csharp
public void UploadScore(int score);
```

and

```csharp
public void UploadScore(int score, int[] details);
```

This will upload a score to the leaderboard for the user, optionally you can provide an array of details.&#x20;

```csharp
public void ForceScore(int score);
```

and

```csharp
public void ForceScore(int score, int[] details);
```

Similar to UploadScore, this will force the user's score to be this new value even if the old score was a better score. This is typically used to reset a user's score on the board.
