---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# IChatMessage

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

A simple interface that standardizes the concept of a chat message making it easier to create UI elements for the presentation and collection of chat messages originating from Steam Lobby, Clan and Friends.

```csharp
using HeathenEngieering.SteamworksIntegration.UI;
```

```csharp
public interface IChatMessage;
```

## Fields and Attributes

### User

```csharp
public UserData User => get;
```

This should return the user that sent this chat message

### Data

```csharp
public byte[] Data => get;
```

This should return the contents of this message as a byte\[] typically this is simply a string that has been encoded with UTF8.

### Message

```csharp
public string Message => get;
```

This should return the contents of the message as a string, this is typically the Data byte\[] encoded to UTF8.

### Type

```csharp
public EChatEntryType TType => get;
```

A enum defined by Steamworks that indicates the type of message. This is not typically used by Unity developers but is required by some Steam API features. Most common value would be k\_EChatEntryTypeChatMsg.

### IsExpanded

```csharp
public bool IsExpanded { get; set; }
```

This should cause the message to expand or contract, for example most use cases call for the message to hide the user's name and icon if the prior message in the collection was from the same user. This reduces UI space used and simplifies rendering. This field will be read and set by Chat Managers and similar controls to cause the detail to expand or contract as required.

### GameObject

```csharp
public GameObject GameObject => get;
```

This should simply return the GameObject this interface is connected to.

## Methods

### Initialize

```csharp
//Initalized from a recieved clan chat message
public void Initialize(ClanChatMsg);

//Initalized from a received lobby chat message
public void Initialize(LobbyChatMsg);

//Initalized from a received friend chat message
public void initialize(UserData sender, string message, EChatEntryType type);
```

These initialization methods will be called by chat managers to initialize the chat record with data received from Steam. While your use case may only require one of them the interface is designed to support all 3.

You should populate the fields of the object when this is called based on the data provided in the arguments.
