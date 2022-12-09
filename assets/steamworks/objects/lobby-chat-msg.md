# Lobby Chat Msg

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct LobbyChatMsg
```

Represents a chat message sent from the Steam Lobby system. This can be used to identify the sending lobby, user and data and can parse the data to a string or Json serialziable object.

### Fields and Attributes

| Type     | Name         | Comment                                 |
| -------- | ------------ | --------------------------------------- |
| Lobby    | lobby        | The source lobby                        |
| UserData | sender       | The user that sent it                   |
| byte\[]  | data         | The raw data sent                       |
| DateTime | recievedTime | The time stamp the message was recieved |
| string   | Message      | the string parsing of the message       |

### Methods

```csharp
public override string ToString();
```

The same as calling Message, this returns the data parsed using UTF8 to a string

```csharp
public T FromJson<T>();
```

This will read the string data into Unity's JsonUtility casting the object to the input type
