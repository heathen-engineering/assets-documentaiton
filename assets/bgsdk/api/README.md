---
description: Documentation on HeathenEngineering.BGSDK.API tools
---

# API

## Introduction

BGSDK's core functionality is defined in the API namespace

```csharp
HeathenEngineering.BGSDK.API
```

The API is broken into 3 core components all of which are statically accessible.

```csharp
HeathenEngineering.BGSDK.API.Tokens
```

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/api/tokens" %}

```csharp
HeathenEngineering.BGSDK.API.User
```

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/api/user" %}

```csharp
HeathenEngineering.BGSDK.API.Wallets
```

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/api/wallets" %}

## Tokens

The API.Tokens class is primarily used during dev time and principally used by the editor tools provided with the kit. It would be unusual to need to use this section of the SDK during run time.

The API.Tokens feature that can be used during run time is the `Get` feature; this feature can also be accessed on the Token artifact type via `Token.Get` . For more information about artifacts, please review the Artifacts article.

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/artifacts" %}

## User

The API.User class is used to authenticate the user with the Arkane system, and populate the `BGSDKSettings.user` identity which is required to be populated before any other feature such as `Wallets` can be used.

## Wallets

The API.Wallets class is the main point of use during run time, and exposes features for creating and managing user wallets and the tokens they contain.
