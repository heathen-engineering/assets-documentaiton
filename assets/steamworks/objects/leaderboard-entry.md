# Leaderboard Entry

## Definition

```csharp
public class LeaderboardEntry
```

Represents an entry found on a leaderboard and contains data about that entry such as the user its related to, details and any attachments.

### Fields and Attributes

| Type                | Name                 | Notes                                             |
| ------------------- | -------------------- | ------------------------------------------------- |
| LeaderboardEntry\_t | entry                | The native entry                                  |
| int\[]              | details              | Details loaded for the entry if any               |
| UserData            | User                 | The user the entry relates to                     |
| int                 | Rank                 | The rank aka position on the board for this entry |
| int                 | Score                | The score for this entry                          |
| UGCHandle\_t        | UgcHandle            | The handle to the attachment if any               |
| bool                | HasCashedUgcFileName | Do we have the file name for this attachment yet  |
| string              | cashedUgcFileName    | The name for the attachment                       |

### Events

#### evtUgcDownloaded

Occurs when the UGC is downloaded.

### Methods

```csharp
public void GetAttachedUgc<T>(callback);
```

{% hint style="info" %}
This starts, updats and completes a UGC download if required and returns the results on the callback in a single line call.
{% endhint %}

This will download the UGC attachment if any and invoke the callback with the results when finished.

```csharp
public bool StartUgcDownload(priority, callback);
```

Starts the process of downloading the UGC attachment if any. Returns false if the attachment handle is invalid e.g. no attachment present

```csharp
public float UgcDownloadProgress();
```

returns the current progres of the UGC download. returns a value between 0 and 1

