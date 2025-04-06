---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Friend List

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

![](<../../../../.gitbook/assets/image (174).png>)

A simple linear list of friends, you can specify via the filter value what types of friends this list should populate. This will update its list when there is an update to persona data detected by Steam client. This means most state changes for a player's friends and followed users will be automatically detected and updated adjusting the list as required.

## Fields and Attributes

### Include Followed

Should the tool include the users that you follow

### Filter

Describes the types of friends that should be included in this list options include

* All\
  Simply lists all friends
* InThisGame\
  Lists friends that are playing this game
* InOtherGame\
  Lists friends that are playing a game but not this one
* InAnyGame\
  Lists friends that are playing any sort of game
* NotInThisGame\
  Lists all friends other than those playing this game
* NotInGame\
  List all friends that are not currently playing a game
* AnyOnline\
  List all friends that are online
* AnyOffline\
  List all friends that are offline
* Away\
  List all online friends that are marked as away
* Buisy\
  List all online friends that are marked as buisy
* Followed\
  List the subset of friends that the local user follows, these may not be "friends" in the since that they may not have accepted a friend invite but are being followed by this player.

### Content

The transform where instantiated records will be parented to

### Record Template

This is a GameObject reference to a template or prefab. The Game Object must have a component on it that implements the [IUserProfile ](../programming-tools/iuserprofile.md)interface.

## Methods

### Clear

Clear the list

```csharp
public void Clear()
```

### Update Display

Update the list display

```csharp
public void UpdateDisplay()
```

### Match Filter

Check the user to determin if it matches the filter configured for this list

```csharp
public bool MatchFilter(UserData friend)
```
