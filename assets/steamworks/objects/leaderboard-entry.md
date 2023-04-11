# Leaderboard Entry

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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

