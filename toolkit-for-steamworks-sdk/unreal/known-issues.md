---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
---

# Known Issues

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Sockets Net Driver

The Sockets Net Driver included in the plugin has a known issue where clients connecting to a Dedicated or Listen server will quickly flash between the spectator and player controller.

The root issue is that possession of the Player Controller is not being acknowledged correctly, this is resulting in the server triggering the rest of the client e.g. the client will spawn all objects, fail to acknowledge correctly, be told to reset and thus destroy all objects only to try again.

### Workaround

There is no current workaround.

It is recommended you work with the default NetDriver while waiting for a proper fix, note that you can disable the Steam Sockets Subsystem so you can use IpNetDriver or similar via the following ini setting.

```ini
[/Script/SteamworksComplete.Steamworkscomplete]
bUseSteamNetworking=False
```

### Community

The [#Unreal Steamworks](https://discord.com/channels/463483739612381204/1153799474620137483) thread in the Discord server is the best place to chat about this topic.
