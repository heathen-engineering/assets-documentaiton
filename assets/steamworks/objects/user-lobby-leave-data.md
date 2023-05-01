# User Lobby Leave Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct UserLobbyLeaveData
```

Used by the Lobby Manager's evtUserLeft event to indicate who left and why.

### Fields and Attributes

| Type                   | Name  | Comment                |
| ---------------------- | ----- | ---------------------- |
| UserData               | user  | The user               |
| EChatMemberStateChange | state | Why did the user leave |

