# Unity Initialization

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><h3>Code Free </h3></td><td><ul><li>Set your desired settings.</li><li>Add a component to the game object</li><li>Done!</li></ul></td></tr><tr><td><h3>With Configuration   </h3></td><td><ul><li>Doesn't require a GameObject</li><li>Single line of code</li></ul></td></tr><tr><td><h3>Pure Code </h3></td><td><ul><li>Doesn't require a GameObject</li><li>No ScriptableObject</li><li>Pure C#</li></ul></td></tr></tbody></table>

## Pure Code

You do NOT require any GameObjects to make Discord Social run. You can simply call our DiscordSocialApp API, and we will handle initialisation of the required objects and optionally start the connection process as soon as ready.

### Namespace

```csharp
using Heathen.DiscordSocialIntegration.API
```

### Initialize

{% hint style="info" %}
You should ask your user before you attempt to connect.&#x20;

A simple way to do this is a "Connect to Discord" button on your main menu or in your settings. When clicked, it should store that the user does want to connect to Discord, and you can use that value in the future to auto-connect.
{% endhint %}

```csharp
DiscordSocialApp.Initialize(123456789987654);
```

Provide your "Client ID", also sometimes called an "Application ID"

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

The second parameter (auto connect) indicates whether or not the system should attempt to connect once initialised. You can set this to false and request a connection on demand later.

### Connect

If you choose to differ connection (passed false into the Initialise function), you will need to call Connect when ready.

{% hint style="info" %}
The first time the app connects to a user's Discord will take focus and ask the user to "Authorise" the app.&#x20;
{% endhint %}

```csharp
DiscordSocialApp.Connect();
```

## Events

The Discord Social SDK initialisation and connection process passes through a number of steps in the background. Each step is represented by a Unity Event you can listen to if desired. All events are part of the DiscordSocialApp static class, the same class you used to call Initialise and Connect.

{% hint style="info" %}
The only event that matters is OnReady, which is triggered when the entire system is ready to be used.
{% endhint %}

Prefer to work in Inspector?\
Have a look at the Discord Event Triggers component. It can expose every system event to you in the inspector.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### OnAuthorizeResult

```csharp
public static UnityEvent<ClientResult, string, string> OnAuthorizeResult
```

Triggers when OAuth authorisation provides the required callbacks.

### OnConnect

```csharp
public static UnityEvent OnConnect
```

Triggers when the system completes the connection.

### OnDisconnect

```csharp
public static UnityEvent OnDisconnect
```

Triggers when the system disconnects from Discord.

### OnReady

```csharp
public static UnityEvent OnReady
```

Triggered when the system state updates to Ready and is thus ready to be used.

### OnReceivedToken

```csharp
public static UnityEvent OnReceivedToken
```

Triggard, when token retrieval completes&#x20;

### OnRetrieveTokenFailed

```csharp
public static UnityEvent OnRetrieveTokenFailed 
```

Triggered when the token request responds with a state of failed.

### OnStatusChanged

```csharp
public static UnityEvent<Client.Status, Client.Error, int> OnStatusChanged
```

Triggers with every system state change, connecting, connected, ready, disconnecting, disconnected, etc.

## Object

When you configured your Discord Social Settings, it created `DiscordSocialSettings` Objects that can be used to initialise directly. The initialisation function on these objects will read all required data from them.

[Configuration Guide](../configuration/unity-configuration.md)

## Component

If you need a code-free solution, we provide you with a component script, `Initialise Discord Social`which will initialise the Steamworks SDK for you based on your configured Steam Settings.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

You DO NOT need to mark this component as Do Not Destroy on Load ... it does not need to persist between levels and only exists to call Initialise for you.

### Authorize and Connect to Discord

```csharp
public void AuthorizeAndConnectToDiscord()
```

Initiates the Discord OAuth authorization flow and connects the user if authorization succeeds.

**Usage**\
Use this in Unity’s Inspector, Unity Events, or visual scripting tools to trigger login and connection without manually handling tokens.

### Connect to Discord with Token

```csharp
public void ConnectToDiscordWithToken(string token, DateTime expirationDate, string refreshToken)
```

Connects to Discord using a pre-obtained access token and refresh token.

**Parameters**

* `token`: The bearer token previously issued by Discord.
* `expirationDate`: The UTC expiration time of the token.
* `refreshToken`: A refresh token used to renew the access token if expired.

**Usage**\
Useful for restoring sessions from previously saved credentials, such as after app relaunch.

### Get Provisional then Connect

```csharp
public void GetProvisionalThenConnect(AuthenticationExternalAuthType externalAuthType, string externalAuthToken)
```

Fetches a provisional token using an external auth provider and connects to Discord if successful.

**Parameters**

* `externalAuthType`: The provider to use (e.g., Steam, Xbox).
* `externalAuthToken`: The auth token issued by the external provider.

**Usage**\
Call this when authenticating through platforms like Steam or Xbox, without going through Discord’s full OAuth flow.

### Get Steam Provisional then Connect

```csharp
public void GetSteamProvisionalThenConnect()
```

{% hint style="success" %}
_Only Available if you have Heathen's Toolkit for Steamworks and/or Steamworks.NET installed_
{% endhint %}

Retrieves a provisional token using a Steam Web API ticket and connects to Discord if successful.

**Usage**\
Designed for games using Steamworks.NET. Automates Steam ticket generation and Discord connection in one call.

### Connect

```csharp
// Callback forms
public void Connect(Action<ErrorType> callback = null)
public void Connect(string token, DateTime expirationDate, string refreshToken, Action<ErrorType> callback = null)

// Task forms
public Task<ErrorType> ConnectTask()
public Task<ErrorType> ConnectTask(string token, DateTime expirationDate, string refreshToken)

// UniTask forms
public UniTask<ErrorType> ConnectUniTask()
public UniTask<ErrorType> ConnectUniTask(string token, DateTime expirationDate, string refreshToken)
```

Triggers Discord connection via OAuth flow or optionally uses an existing token set then connects.

**Optional Parameters**

* `token`: The Discord bearer token.
* `expirationDate`: The UTC expiration time of the token.
* `refreshToken`: The refresh token used to renew the token.

### Get Provisional Token

```csharp
public void GetProvisionalToken(AuthenticationExternalAuthType externalAuthType, string externalAuthToken, Client.TokenExchangeCallback callback = null)
```

Fetches a provisional token from an external auth source.

**Parameters**

* `externalAuthType`: Auth provider (Steam, Xbox, etc.)
* `externalAuthToken`: Token from the provider.
* `callback`: Optional callback to receive token exchange result.

**Usage**\
Use in cases where the auth flow begins with an external provider instead of Discord.

### Get Steam Provisional Token

```csharp
public void GetSteamProvisionalToken(Client.TokenExchangeCallback callback = null)
```

{% hint style="success" %}
_Only Available if you have Heathen's Toolkit for Steamworks and/or Steamworks.NET installed_
{% endhint %}

Retrieves a provisional token using a Steam Web API ticket.

**Parameters**

* `callback`: Optional callback with result and token details.

**Usage**\
Use in Steam games that authenticate through Steam rather than Discord OAuth.
