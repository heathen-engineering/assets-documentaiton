---
description: BGSDK Authentication examples
---

# Authenticate the user

## Introduction

For more information on Authentication please refer to the User API article

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/api/user" %}

In all cases you will be using a 3rd party to handle authentication and using the BGSDK to exchange that authentication token for an "identity". Once authenticated, the identity is valid for a finite period and must be refreshed or otherwise renewed periodically.‌

Considering the BGSDK is primarily used to read the user's wallet, you will typically make infrequent calls to the API; as such you will typically refresh the authentication immediately before any major client-side transactions, perform all desired transactions in bulk, and cache the results in game memory. This reduces the duration of API exchange and reduces the likelihood of the token being expired on API call.

{% hint style="info" %}
Minting and exchanging tokens would be handled by a trusted server and not performed in Unity via the BGSDK, and as such are not affected by the client-side authentication.
{% endhint %}

## Use Cases

### Web Authentication

In this use case you are using a web authentication outside of the game to perform authentication and will need to pass that token into the game and register it with the BGSDK.

The advantage of this method is handling the authentication via a web app or site, where you can also handle account creation, license notification and similar in a rich user experience.&#x20;

The disadvantage is that you need to build and manage a web enabled app/site to serve as the user interface.

Once you have the authentication token and have communicated it to your game, you can use the following logic to register that token with the BGSDK. This assumes you have the following information from the authentication process

* accessToken\
  A string value representing the Venly token returned by the Web API
* expiresIn\
  An integer value provided by the Web API regarding expiration of the token
* refreshToken\
  A string value representing the Venly refresh token returned by the Web API
* refreshExpiresIn\
  An integer value provided by the Web API regarding expiration of the refresh token

```csharp
API.User.Login_3rdPartyAuthentication(DateTime.Now, 
    accessToken,
    expiresIn,
    refreshToken,
    refreshExpiresIn);
```

### Facebook Authentication

In this use case you are using Facebook as the authentication provider and need to exchange a Facebook authentication token for a Venly authentication. The BGSDK has a built in feature for this provided in the User API.

The advantage of this method is offloading the responsibility and security risks of authentication to a 3rd party

The disadvantage of this method is dependency on a 3rd party

You only need to provide the Facebook token as provided to you by your Facebook authentication provider.

{% hint style="warning" %}
This is an asynchronous action so must be performed as a co-routine in Unity
{% endhint %}

```csharp
StartCoroutine(API.User.Login_Facebook(token, (requestState) =>
    {
        if (!requestState.hasError)
        {
            Debug.Log("User is Authenticated");
        }
    }));
```

### Steam Authentication

{% hint style="warning" %}
Authentication via Steam Authentication API is possible, but requires you work with Venly directly.
{% endhint %}

### PlayFab (Microsoft) Authentication

{% hint style="warning" %}
Authentication via PlayFab Authentication is possible, but requires you work with Venly directly.
{% endhint %}

### GameLift (Amazon) Authentication

{% hint style="warning" %}
Authentication via GameLift Authentication is possible, but requires you work with Venly directly.
{% endhint %}

### Discord Authentication

{% hint style="warning" %}
Authentication via Discord API is possible, but requires you work with Venly directly.
{% endhint %}

### Google Authentication

{% hint style="warning" %}
Authentication via Google Authentication is possible, but requires you work with Venly directly.
{% endhint %}
