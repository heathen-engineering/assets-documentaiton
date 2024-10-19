---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Leaderboard Entry

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class LeaderboardEntry
```

Represents an entry found on a leaderboard and contains data about that entry such as the user its related to, details and any attachments.

## Fields and Attributes

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

## Events

### evtUgcDownloaded

Occurs when the UGC is downloaded.

## Methods

### Get Attachment

```csharp
public void GetAttachedUgc<T>(callback);
```

{% hint style="info" %}
This starts, updats and completes a UGC download if required and returns the results on the callback in a single line call.
{% endhint %}

This will download the UGC attachment if any and invoke the callback with the results when finished.

### Start UGC Download

```csharp
public bool StartUgcDownload(priority, callback);
```

Starts the process of downloading the UGC attachment if any. Returns false if the attachment handle is invalid e.g. no attachment present

### UGC Download Progress

```csharp
public float UgcDownloadProgress();
```

returns the current progres of the UGC download. returns a value between 0 and 1

