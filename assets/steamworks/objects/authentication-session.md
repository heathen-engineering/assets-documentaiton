# Authentication Session

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class AuthenticationSession
```

Used by the [Authentication ](../api/authentication.md)interface to represent an active authentication session

## Fields and Attributes

| Type                 | Name            | Comment                                                                                   |
| -------------------- | --------------- | ----------------------------------------------------------------------------------------- |
| bool                 | isClientSession | Is this a client or server session                                                        |
| CSteamID             | user            | The ID typically a user the session is related to                                         |
| CSteamID             | gameOwner       | The id of the owner of the game, if this is different than the user then this is barrowed |
| byte\[]              | data            | the ticekt data that was used to start the session                                        |
| EAuthSessionResponse | responce        | The responce recieved when validating a provided ticket                                   |
| bool                 | IsBarrowed      | The same as user == gameOwner                                                             |
| Action               | onStartCallback | the callback invoked when the session has started ... this is used internally             |

## Methods

### End

```csharp
public void End();
```

Ends this session&#x20;
