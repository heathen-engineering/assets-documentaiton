---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Steam Game Server Events

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Exposes Steam Game Server events to the Unity Inspector

## Definition

```csharp
public class SteamGameServerEvents : MonoBehaviour
```

## Events

### evtDisconnected

Occurs when the game server disconnects from the Steam API

### evtConnected

Occurs when the game server connects to Steam API

### evtFailure

Occures when Steam API notifies the game server of a failure
