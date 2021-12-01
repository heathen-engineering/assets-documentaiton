---
description: HeathenEngineering.BGSDK.API.User
---

# User

{% hint style="warning" %}
2021-10-05

The Venly authentication methods are temporarily deprecated as per Venly request. If you have any questions or need more support around authentication through the Venly APIs please contact Venly.
{% endhint %}

```csharp
HeathenEngineering.BGSDK.API.User
```

A wrapper around user features such as authentication and user data.

{% embed url="https://docs.arkane.network/api/authentication/authentication" %}

## Overview

The User static class is primarily used to authenticate the current user against the Arkane backend service.&#x20;

{% hint style="warning" %}
You can only perform API actions after a user has been authenticated. The system stores the authenticated user in memory at:

```csharp
public static Identity BGSDKSettings.user;
```

This is used by all other methods from its static accessor.
{% endhint %}

## Get Profile

```csharp
public static IEnumerator GetProfile(Action<UserProfileResult> callback);
```

Returns data related to the authenticated user via the UserProfile object.

### Examples

These examples assume you are familiar with the use of Unity Co-routines and the basics of C# in the context of Unity.

```csharp
StartCoroutine(API.User.GetProfile((requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("Found " + requestState.result.username+ "'s profile");
        }
    }));
```

## Login 3rd Party Authentication

Sets the `BGSDKSettings.user` to the authenticated identify as provided in the input parameters of this method.

```csharp
public static void Login_3rdPartyAuthentication(DateTime createdAt,
    string accessToken,
    int expiresIn,
    string refreshToken,
    int refreshExpiresIn);
```

This is used to record an authentication token acquired from a 3rd party source, such as a web pass through in Unity memory for use on subsequent API calls. In order to use this you will need to use the Arkane Web API or similar method by which you can retrieve a valid Arkane access token.

### Examples

```csharp
API.User.Login_3rdPartyAuthentication(DateTime.Now, 
    accessToken,
    expiresIn,
    refreshToken,
    refreshExpiresIn);
```

## Login Facebook

Sets the `BGSDKSettings.user` to the authenticated identify as provided in the input parameters of this method.

```csharp
public static IEnumerator Login_Facebook(string token, 
    Action<AuthenticationResult> callback);
```

Exchanges a Facebook identity token via the Arkane Web API, this assumes you already have a Facebook identity token.

### Examples

```csharp
StartCoroutine(API.User.Login_Facebook(token, (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("User is Authenticated");
        }
    }));
```
