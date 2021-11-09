# Rank Change

## Definition

```csharp
public struct RankChange
```

Used by the Leaderboard system when a user's rank changes.

### Fields and Attributes

| Type                | Name            | Comment                                      |
| ------------------- | --------------- | -------------------------------------------- |
| string              | leaderboardName | The name of the board                        |
| SteamLeaderboard\_t | leaderboardId   | The id of the board                          |
| LeaderboardEntry    | oldEntry        | The prior entry data                         |
| LeaderboardEntry    | newEntry        | The current entry data                       |
| int                 | rankDelta       | The amount of change in rank e.g. new - old  |
| int                 | scoreDelta      | The amount of change in score e.g. new - old |

