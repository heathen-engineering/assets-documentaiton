---
description: The leader in board 👍
---

# Leaderboard Manager

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

## Introduction

Meant to be added to a game object at or near your leaderboard UI, this behaviour can help you display leaderboard entries and simplifies the process of uploading scores to a leaderboard.

## Definition

### Fields and Attributes

| Type              | Name               | Comment                                       |
| ----------------- | ------------------ | --------------------------------------------- |
| LeaderboardObject | leaderboard        | The leaderboard this manager should work with |
| LeaderboardEntry  | LastKnownUserEntry |                                               |

### Events

#### evtUserEntryUpdated

Occurs when the local user's last known user entry is updated. This can only be raised by operations ran from within the Leaderboard Manager ... for example if you call the RefreshUserEntry or GetUserEntries. Then it is likely to be raised assuming the local user has an entry however if you manually query the board using API.Leaderboards or other methods it will not be raised.

#### evtQueryCompleted

Occurs when a query for records complets and contains the results of that query

#### evtQueryError

Occurs when a query fails with an error, errors are not generally specified rather it is up to you to check for logicle causes such as the leaderboard being null or not being valid.

#### evtUploadError

Occurs when an attempt to upload scores fails. As with query errors the API doesn't usually provide any additional information. The typical causes are an invalid board or a board that can only be set by the Web API

### Methods

```csharp
public void RefresshUserEntry();
```

Queries the board for the local user's entry.

```csharp
public void GetTopEntries(int count);
```

Queries the board for the top X number of entries.

```csharp
public void GetNearbyEntries(int beforeUser, int afterUser);
```

Queries the board for entries around the player, before is the number entries before the player's entry and after is the number after the user's entry.

{% hint style="info" %}
Both values should be entered as positive whole numbers.
{% endhint %}

```csharp
public void GetAllFriendsEntries();
```

This will return all entries for all friends that have an entry in this board.

```csharp
public void GetUserEntries(IEnumerable<UserData> users);
```

This will return entries for each of the indicated user's if they have an entry to return.

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
