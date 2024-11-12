---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Friend Invite Dropdown

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Displays a list of the clans the user sees e.g. is a member of or otherwise has a relationship with.

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class FriendInviteDropDown : MonoBehaviour
```

## Events

### Invited

A User Data event that will be invioked when the "invite" button is pressed for a specific friend. The event will indicate for what friend the button was pressed

```csharp
public UserDataEvent Invited;
```

The handler for this event would take the form of

```csharp
void Handler(UserData user)
{
    //Do Work
}
```

## Fields and Attributes

### Filter

A set of flags that indicate what friends should be included in the list

```csharp
public FilterOptions filter;
```

This uses an internal struct

```csharp
public struct FilterOptions
{
    public bool inThisGame;
    public bool inOtherGame;
    public bool busy;
    public bool away;
    public bool snooze;
}
```

* In This Game\
  Should friends that are playing the current game be displayed
* In Other Game\
  Should friends that are playing some other game be displayed
* Busy\
  Should friends with a persona state of busy be displayed
* Away\
  Should friends with a persona state of away be displayed
* Snooze\
  Should friends with a persona state of snooze be displayed

## Methods

### Show

Expands the drop down and displays the list of friends that match the filter

```csharp
public void Show()
```
