# Lobby Chat Msg

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct LobbyChatMsg
```

Represents a chat message sent from the Steam Lobby system. This can be used to identify the sending lobby, user and data and can parse the data to a string or Json serialziable object.

### Fields and Attributes

<table><thead><tr><th width="187.56643368118847">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>Lobby</td><td>lobby</td><td>The source lobby</td></tr><tr><td>UserData</td><td>sender</td><td>The user that sent it</td></tr><tr><td>byte[]</td><td>data</td><td>The raw data sent</td></tr><tr><td>DateTime</td><td>recievedTime</td><td>The time stamp the message was recieved</td></tr><tr><td>string</td><td>Message</td><td>the string parsing of the message</td></tr></tbody></table>

### Methods

```csharp
public override string ToString();
```

The same as calling Message, this returns the data parsed using UTF8 to a string

```csharp
public T FromJson<T>();
```

This will read the string data into Unity's JsonUtility casting the object to the input type
