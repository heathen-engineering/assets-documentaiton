# Clan Chat Msg

## Definition

```csharp
public struct ClanChtMsg
```

Represents a chat message from the [Clans ](../api/clans.client.md)interface

## Fields and Attributes

### room

```csharp
public ChatRoom room;
```

The room this message relates to

### type

```csharp
public EChatEntryType type;
```

The type of chat entry this is

### message

```csharp
public string message;
```

The message body

### user

```csharp
public UserData user;
```

The user this message came from
