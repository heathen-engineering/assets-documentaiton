# User Lobby Leave Data

## Definition

```csharp
public struct UserLobbyLeaveData
```

Used by the Lobby Manager's evtUserLeft event to indicate who left and why.

### Fields and Attributes

| Type                   | Name  | Comment                |
| ---------------------- | ----- | ---------------------- |
| UserData               | user  | The user               |
| EChatMemberStateChange | state | Why did the user leave |

