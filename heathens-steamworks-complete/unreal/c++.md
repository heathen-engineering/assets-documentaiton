# C++

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Heathen's Steamworks Complete is always built on the full raw Steam API for every engine and Unreal Steamworks Complete is no different.

You can access the entire Steam Client and Steam Game Server API fro C++ with minimal effort using our asset.

## Step 1

Add Steamworks Complete to your public dependency module names in your project Build.cs

```cpp
PublicDependencyModuleNames.AddRange(new string[] 
{ 
    "Core", 
    "CoreUObject", 
    "Engine", 
    "InputCore", 
    "SteamworksComplete" 
});
```

## Step 2

Reference the required headers

```cpp
THIRD_PARTY_INCLUDES_START
#include <SteamworksComplete/sdk/steam_api.h>
THIRD_PARTY_INCLUDES_END
```

The full SDK's headers have been included with all assemblies accounted for including support for&#x20;

* Mac
* Linux
* Windows 64

## Step 3

You now have the box standard Steamworks SDK's Steam API at your disposal exactly as Valve intended it.&#x20;

Valve's Steamworks SDK is an older C-styled kit, see our Blueprints for an easier approach or review there source code for functional examples of working with Steam API covering every method, callback and call result.
