# Authentication Ticket

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class AuthenticationTicket
```

Used by the [Authentication ](../api/authentication.md)interface to represent an active authentication ticket

## Fields and Attributes

<table><thead><tr><th width="176.1867087633845">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>bool</td><td>isClientTicket</td><td>Is this a client or server ticket</td></tr><tr><td>HAuthTicket</td><td>handle</td><td>The auth ticket handle used internally</td></tr><tr><td>byte[]</td><td>data</td><td>ticket data</td></tr><tr><td>bool</td><td>verified</td><td>has this ticket been verified, this gets set to true when the Get Authentication Session responce comes in</td></tr><tr><td>uint</td><td>createdOn</td><td>the date this ticekt was created on</td></tr><tr><td>EResult</td><td>result</td><td>EResult state from the ticket request</td></tr></tbody></table>

## Methods

### Cancel

```csharp
public void Cancel();
```

Cancels this ticket
