# Clan Chat Msg

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct ClanChtMsg
```

Represents a chat message from the [Clans ](../api/clans.md)interface

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
