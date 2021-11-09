# Lobby Member

## Definition

```csharp
public struct LobbyManager
```

Represents a user in a given lobby.

### Fields and Attributes

| Type     | Name          | Comment                                                                                               |
| -------- | ------------- | ----------------------------------------------------------------------------------------------------- |
| Lobby    | lobby         | The lobby this user belongs to                                                                        |
| UserData | user          | The user this member represents                                                                       |
| string   | \[string key] | <p>Gets metadata about this user. </p><p>This user can use this to set metadata values as well</p>    |
| bool     | IsReady       | Gets or sets the ready flag, only the user its self can set this value                                |
| string   | GameVersion   | Gets or sets the version of the game this user is running. Only the user its self can set this value. |

### Methods

```csharp
public string this[string key];
```

Can be used to get or set metadata values on this user. Only the user its self can set metadata values.

```csharp
public void Kick();
```

Kick this user from this lobby using the Heathen Kick list
