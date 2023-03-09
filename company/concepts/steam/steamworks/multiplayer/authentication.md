---
description: >-
  Understanding Steam Authentication, when and why to use it ... and when and
  why not to.
---

# Authentication

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../">Guides and Tutorials</a></td><td><a href="../../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../../assets/physkit/">physkit</a></td><td><a href="../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../../assets/ux/">ux</a></td><td><a href="../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% embed url="https://partner.steamgames.com/doc/features/auth" %}

{% hint style="info" %}
The above link and repeated below so you can find it:\
[https://partner.steamgames.com/doc/features/auth](https://partner.steamgames.com/doc/features/auth)\
\
Is highly important, you should fully read Valve's own documentation around Steam Authentication to fully understand it. Some of the information will be summarized here in and notes on the tools and systems Heathen has created around Steam Authentication.&#x20;
{% endhint %}

## Authentication API

Heathen's Authentication API handles both Client and Server authentication and manages the ticket and session data generated for you.

{% embed url="https://kb.heathenengineering.com/assets/steamworks/api/authentication" %}

You will notice that unlike other APIs there is no Client or Server or Web version. Because the Steam API end points have the same requirements and signatures for all targets we are able to select the correct end point for you based on the build type.

That is for a client or "normal" build we will use the Client end points and for a server build or "headless" build we will use the Server end points.

## Workflow

The intended use of Steam Authentication is that the subject who wishes to authenticate ... typically a user. Will generate a "Ticket"&#x20;

### Generate Ticket

[Get Auth  Session Ticket](../../../../../assets/steamworks/api/authentication.md#getauthsessionticket)

```csharp
Authentication.GetAuthSessionTicket((ticket, IOError) =>
{
    if(!IOError)
    {
        SendToServer(UserData.Me, ticket.data);
    }
});
```

This ticket contains a bit of information but the important part is the data represented as a byte\[]

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/authentication-ticket" %}

This is the data that should be sent to who or whatever it is that will be authenticating this subject. So send it to your game server or your peer if your doing peer to peer authentication ... and yes peer to peer authentication can be done.

### Send Ticket

How exactly you send the ticket is between you and your networking tool or your lobby system.&#x20;

{% hint style="success" %}
For example in a Peer to Peer game where you are using Steam Inventory items you may want to validate that all members of a lobby do really own the items they claim to own. You can use Steam Authentication for this by starting an authentication session between each user and sending a serialized copy of the inventory items. Steam client can then validate that yes they are owned and who they are owned by.
{% endhint %}

In any case you will need to send 2 bits of information being&#x20;

1. The user ID of the user who generated the ticket
2. The byte\[] e.g. "Ticket Data" that was generated

{% hint style="info" %}
Each ticket can be used exactly once and does expire after a period of time. So for example if you want to have every peer in a P2P game authenticate every other peer then every player will need to generate 1 ticket for every other player and will need to validate 1 ticket from every other player.
{% endhint %}

### Begin Auth Session

[Begin Auth Session](../../../../../assets/steamworks/api/authentication.md#beginauthsession)

```csharp
void AuthenticatUser(byte[] ticket, UserData user)
{
    var responce = Authentication.BeginAuthSession(ticket, user, result =>
    {
        switch(result.responce)
        {
            case EAuthSessionResponse.k_EAuthSessionResponseOK:
                //All is well
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseUserNotConnectedToSteam:
                //This user is not connected to Steam
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseNoLicenseOrExpired:
                //This user is not licensed for this game
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseVACBanned:
                //This user is VAC banned for this app
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseLoggedInElseWhere:
                //This session is logged elsewhere
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseVACCheckTimedOut:
                //This VAC Check is timed out, may be fine, may not
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketCanceled:
                //This Tickedt cancled by owner
            break;
            case EAuthSessionResponse.k_EAuthSessionResponsePublisherIssuedBan:
                //This publisher issued ban
            break;
            
            case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketInvalidAlreadyUsed:
                //This Ticket invalid / already used
            break;
            
            case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketInvalid:
                //This Ticket invalid
            break;
        }
    });
    
    switch(responce)
    {
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultOK:
            //Send correctly, wait for callback
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultInvalidTicket:
            //Invalid ticket, will get no responce
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultDuplicateRequest:
            //Duplicate request, will get no responce
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultInvalidVersion:
            //Invalid version, will get no responce
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultGameMismatch:
            //Game missmatch, will get no responce
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultExpiredTicket:
            //Expired ticket, will get no responce
        break;
    }
}
```

This simply takes in the ticket and user ID that generated it and asks Steam API to validate it. The results of this call will tell you rather or not its valid and will give you details about the authenticated user such as rather or not they are VAC banned, how exactly they own a license to the App they are authenticating from and for, etc.

Having authenticated a user allows for a few additional features. For example a Steam Game Server identifies the users playing on it by what Auth Sessions are active. That is when you Begin Auth Session for a user you are telling Valve that said user is playing on that server, when you end the session you are telling Valve that user is no longer playing.

### End Auth Session

[End Auth Session](../../../../../assets/steamworks/api/authentication.md#endauthsession)

```csharp
void UserLoggedOff(UserData user)
{
    Authentication.EndAuthSession(user);
}
```

When a game session is done you should notify Valve that the session is over by ending the auth session.

## Inventory

A common use for authentication sessions is to validate that a given user owns specific inventory items. This can only be done once an Authentication Session has been started with that user. This can be done on Client to Client or Client to Server.

You can either serialize the local user's whole inventory (rare)

[Serialize All Item Results](../../../../../assets/steamworks/api/inventory.md#serializeallitemresults)

or you can serialize specific items (more common)

[Serialize Item Results By ID](../../../../../assets/steamworks/api/inventory.md#serializeitemresultsbyid)

In either case the result is a byte\[] of data that represents the inventory state at the time of serialization, who that inventory was read from and when it was read.

```csharp
//Assume that instanceIds is the collection of items you want to send
SteamItemInstnaceID_t[] instanceIds;

Inventory.Client.SerializeItemResultsByID(instanceIds, data =>
{
    SendDataToRequestingParty(UserData.Me, data);
});
```

Once you have this byte\[] you should send it to who or whatever it is that needs to validate ownership of the items.

The specifics of sending the data is between you and your networking tools, the important thing is that you are sending 2 bits of data

1. The user ID who generated the serialized inventory data
2. The data its self

When your peer or server receives this data they can read its details

[Deserialize Result](../../../../../assets/steamworks/api/inventory.md#destroyresult)

```csharp
void ValidateInventory(UserData user, byte[] data)
{
    Inventory.Client.DeserializeResult(user, data, responce =>
    {
        if(responce.result == EResult.k_EResultOK)
        {
            Debug.Log(user.Nickname + " owns these " + items.length + " items");
        }
        else if(responce.result == EResult.k_EResultExpired)
        {
            Debug.LogWarning(user.Nickname + " owns them, but this data is old.");
        }
    });
}
```

