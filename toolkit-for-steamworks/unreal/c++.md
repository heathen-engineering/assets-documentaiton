---
cover: ../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# C++

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Working in C++ then add this to your Build.cs

```csharp
PrivateDependencyModuleNames.AddRange(
    new string[]
    {
        //... your other dependencies
        "Steamworks",
    });

//This is important to
AddEngineThirdPartyPrivateStaticDependencies(Target, "Steamworks");
```

now in code, you should be able to do this

```cpp
THIRD_PARTY_INCLUDES_START
#include <steam/steam_api.h>        //For client APIs
#include <steam/steam_gameserver.h> //For server APIs
THIRD_PARTY_INCLUDES_END
```

Heathen's Steam Game Instance includes this for you and comes with a slew of helpful tools such as exposing all the callbacks to events and defining linker wrappers enabling a more modern callback structure than the native Steamworks SDK was set up for.

To access it in code, simply add it to your dependencies:

```csharp
PrivateDependencyModuleNames.AddRange(
    new string[]
    {
        //... your other dependencies
        "ToolkitSteamworks",
    });
```

You should now be able to access SteamGameInstance and HeathenTools, its worth noting that Unreal Editor would do this for you. To do so, in the editor click Add C++ object and choose the parent class of SteamGameInstance. You'll often want to create a derived instance anyway especially when working in C++ as this acts as your most global instanced object initializing right after engine load.
