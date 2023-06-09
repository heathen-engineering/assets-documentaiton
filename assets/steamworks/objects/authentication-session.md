# Authentication Session

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class AuthenticationSession
```

Used by the [Authentication ](../api/authentication.md)interface to represent an active authentication session

## Fields and Attributes

<table><thead><tr><th width="176.1867087633845">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>bool</td><td>isClientSession</td><td>Is this a client or server session</td></tr><tr><td>CSteamID</td><td>user</td><td>The ID typically a user the session is related to</td></tr><tr><td>CSteamID</td><td>gameOwner</td><td>The id of the owner of the game, if this is different than the user then this is barrowed</td></tr><tr><td>byte[]</td><td>data</td><td>the ticekt data that was used to start the session</td></tr><tr><td>EAuthSessionResponse</td><td>responce</td><td>The responce recieved when validating a provided ticket</td></tr><tr><td>bool</td><td>IsBarrowed</td><td>The same as user == gameOwner</td></tr><tr><td>Action</td><td>onStartCallback</td><td>the callback invoked when the session has started ... this is used internally</td></tr></tbody></table>

## Methods

### End

```csharp
public void End();
```

Ends this session&#x20;
