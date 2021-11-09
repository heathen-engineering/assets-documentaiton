# Favorite Game

## Definition

```csharp
public struct FavoriteGame
```

Used by the [Matchmaking ](../api/matchmaking.md)interface in relation to favorite game servers.

### Fields and Attributes

| Type     | Name               | Comment                                     |
| -------- | ------------------ | ------------------------------------------- |
| AppId\_t | appId              | The ID of the game                          |
| string   | IpAddress          | string representation of the IP address     |
| uint     | ipAddress          | Steam native uint version of the IP address |
| ushort   | connectionPort     |                                             |
| ushort   | queryPort          |                                             |
| DateTime | lastPlayedOnServer |                                             |
| bool     | isHistory          |                                             |

