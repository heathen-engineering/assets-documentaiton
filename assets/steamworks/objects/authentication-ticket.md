# Authentication Ticket

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class AuthenticationTicket
```

Used by the [Authentication ](../api/authentication.md)interface to represent an active authentication ticket

## Fields and Attributes

| Type        | Name           | Comment                                                                                                    |
| ----------- | -------------- | ---------------------------------------------------------------------------------------------------------- |
| bool        | isClientTicket | Is this a client or server ticket                                                                          |
| HAuthTicket | handle         | The auth ticket handle used internally                                                                     |
| byte\[]     | data           | ticket data                                                                                                |
| bool        | verified       | has this ticket been verified, this gets set to true when the Get Authentication Session responce comes in |
| uint        | createdOn      | the date this ticekt was created on                                                                        |
| EResult     | result         | EResult state from the ticket request                                                                      |

## Methods

### Cancel

```csharp
public void Cancel();
```

Cancels this ticket
