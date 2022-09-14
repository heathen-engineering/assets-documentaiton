# Lobby Member

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

LobbyMember is a structure that wraps around Lobby and UserData to simplify access to the lobby member metadata and related features for a specific user on a specific lobby. In most cases you would be working with the LobbyMember of the local user and can easily create the LobbyMember by reading it from the related lobby.

```csharp
//Assuming we have a Lobby named myLobby
//We can get our LobbyMember by reading the me field
LobbyMember lobbyMember = myLobby.Me;
```

The most common thing to do with a LobbyMember is to set the [metadata](../features/multiplayer/matchmaking-tools.md#metadata) of that member.

```csharp
lobbyMember["fieldName"] = "fieldValue";
```

{% hint style="info" %}
You can learn more about Lobby metadata and LobbyMember metadata by reading [this](../features/multiplayer/matchmaking-tools.md#metadata) article.
{% endhint %}

## Definition

```csharp
public struct LobbyManager
```

Represents a user in a given lobby.

{% hint style="warning" %}
This structure does not store any data locally, it is simply a means by which you can simplify the reading and writing of data to and from a LobbyMember ...&#x20;



For example to read the metadata of a field on a user you typically need to know the Lobby's ID and the User's ID and then call the API such as&#x20;

```csharp
var value = API.Matchmaking.Client.GetLobbyMemberData(lobby, user, metadataKey);
```



As you can see this is long and easily make a mistake with and so by using this tool we can simplify that as.



```csharp
var value = lobbyMember[metadataKey];
```
{% endhint %}

You can get a list of the LobbyMember's in a Lobby or you can create the LobbyMember assuming you know the Lobby ID and the User's ID i.e.

```csharp
var myMember = new LobbyMember { lobby = thisLobby, user = UserData.Me };
```

Is the exsact same data as

```csharp
var myMember = thisLobby.User;
```

which is the same data as

```csharp
var myMember = thisLobby.Members.First(p => p.user = UserData.Me);
```

### lobby

The ID of the lobby this member is a member of

```csharp
public Lobby lobby;
```

### user

The ID of the user this represents

```csharp
public UserData user;
```

### IsReady

A shortcut to read or write the user's lobby member metadata for the field `z_heathenReady`

```csharp
public bool IsReady { get; set; }
```

This is the same as calling&#x20;

```csharp
lobbyMember["z_heathenReady"] = value.ToString();
```

to set a value or

```csharp
var valueAsBool = bool.Parse(lobbyMember["z_heathenReady"]);
```

The read the value as a bool

### GameVersion

A shortcut to read or write the user's lobby member metadata for the field `z_heathenGameVersion`

This is the same as calling&#x20;

```csharp
lobbyMember["z_heathenGameVersion"] = versionAsString;
```

to set a value or

```csharp
var versionAsString = bool.Parse(lobbyMember["z_heathenGameVersion"]);
```

The read the value as a bool



## Methods

### this\[string key]

```csharp
public string this[string key];
```

Can be used to get or set metadata values on this user. Only the user its self can set metadata values.

### Kick

```csharp
public void Kick();
```

Kick this user from this lobby using the Heathen Kick list
