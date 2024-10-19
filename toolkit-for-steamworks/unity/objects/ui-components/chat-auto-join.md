---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Chat Auto Join

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Can be connected to a GameObject along with the [Clan Chat Director](clan-chat-director.md) to cause the system to automatically join the clan chat on start up.

## Fields and Attributes

### ClanId

The ID of the clan that should be joined, this is a ulong value that can usually be found as part of the URL of a clan or similar. You could optionally search for clans using the Clan API and use the ID found there.

This field is private but can be set in the Unity Editor.

```csharp
[SerializeField]
private ulong clanId;
```
