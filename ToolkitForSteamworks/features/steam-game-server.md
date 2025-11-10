# Steam Game Server

### What it is

A **Steam Game Server** is a specialised configuration of a game build designed to interface with Steam’s backend services for multiplayer titles. Unlike a client build, which is designed for players to interact with directly, a game server build runs headless—without UI—and focuses entirely on hosting and managing multiplayer sessions.

At its core, a Steam Game Server is responsible for:

* **Facilitating online multiplayer** by managing session data and player connections.
* **Enabling discovery** through integration with the **Steam Game Server Browser**.
* **Providing telemetry** such as player counts, game modes, and maps.
* **Supporting features** like **VAC (Valve Anti-Cheat)** and **community visibility**.

### What It Is Not

It's important to understand that a Steam Game Server is:

* **Not a dedicated matchmaker**—Steam provides matchmaking APIs, but it’s up to your game to define how players are grouped.
* **Not mandatory** for peer-to-peer games—though registering a P2P session as a "server" can still enable listing, visibility, and access to telemetry/statistics features.
* **Not a server host**—you still need to provide or rent infrastructure to run the server builds (e.g., via AWS, GPortal, PlayFab, or self-hosting).

### Why Use a Steam Game Server?

While not required for all games, Steam Game Servers offer a number of advantages:

* **Public Listing**: Appear in the Steam Game Server Browser, making your servers discoverable to players.
* **Security**: Integrate VAC to help secure gameplay sessions from cheating.
* **Scalability**: Support large-scale multiplayer via server clusters and matchmaking integration.
* **Stats and Telemetry**: Gather information about player activity and server health.
* **Community Presence**: Gain visibility across the broader Steam ecosystem, helping players find and join active games.

Steam Game Servers form the backbone of many online titles—from fast-paced shooters to sandbox RPGs—and understanding their setup and capabilities is key to delivering a reliable multiplayer experience.

## Core Concepts

Understanding how Steam Game Servers function requires familiarity with a few key concepts. These govern how your server connects to Steam, is listed to players, and interacts with Valve’s backend systems.

### Steam Game Server vs Steam Client

The **Steam Game Server** is a headless build configured to use the server variant of the Steam API (`SteamGameServer` interfaces), while the **Steam Client** build uses the standard client interfaces. These are mutually exclusive in code and behaviour—servers manage sessions and respond to queries, clients join and participate.

When properly compiled (e.g. using `UNITY_SERVER` or Unreal’s server build target), your game will automatically initialise the correct API interfaces based on context.

### Anonymous Login vs Authenticated Login

* **Anonymous Login**
  * The recommended and most common approach.
  * No GSLT (Game Server Login Token) is required.
  * Automatically allows your server to appear in the public Steam Server Browser (provided you call `SetAdvertiseServerActive(true)` and set a server name).
  * Only limitation: you cannot bind the server to a specific Steam account, so metrics or server-owned inventory features tied to a Steam account won’t apply.
* **Authenticated Login (GSLT)**
  * Still supported, but usually only needed if you want to tie this server instance to a particular Steam user or enable “server-owned” features (e.g. remote access to a server’s inventory or workshop rights).
  * Requires a valid GSLT issued via your Steamworks partner portal.
  * Provides identical visibility in the public browser (again, as long as you advertise).
  * Can be revoked centrally if abused—useful if you need to “own” the server under a particular account.

**In practice:** most servers simply call `SteamGameServer.LogOnAnonymous()` and then `SetAdvertiseServerActive(true)`. That’s all you need to get the full listing, VAC support, player counts, etc., without ever touching a GSLT.

### Advertise vs Non-Advertise Modes

After logging in, a server can toggle whether it's **advertised** to the public Steam server listing:

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

<figure><img src="../.gitbook/assets/image (364).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
SteamGameServer.SetAdvertiseServerActive(true);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (365).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
SteamGameServer()->SetAdvertiseServerActive(true);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
SteamGameServer.SetAdvertiseServerActive(true);
```
{% endtab %}
{% endtabs %}

If `AdvertiseServerActive` is **false**, your server will not appear in the Steam Game Server Browser, even if logged in with a valid GSLT. This toggle allows you to dynamically control visibility (e.g. during maintenance or in private test sessions).

### Steam App ID and GSLT (Game Server Login Token)

Your **Steam App ID** is the unique identifier Valve assigns to your game. It’s required for any Steamworks API call—both client and server builds must reference the correct App ID during initialization so Steam knows which game is being hosted [partner.steamgames.com](https://partner.steamgames.com/doc/features/multiplayer/game_servers?utm_source=chatgpt.com). Typically, you place this App ID in a `steam_appid.txt` file alongside your server executable (or embed it in your binary via build scripts).

A **Game Server Login Token (GSLT)** is separate from the App ID but is tied to it. In modern Steamworks usage, you do **not** need a GSLT just to appear in the public server browser—calling `SteamGameServer.LogOnAnonymous()` with a valid App ID is sufficient to register and list the server [partner.steamgames.com](https://partner.steamgames.com/doc/features/multiplayer/game_servers?utm_source=chatgpt.com). A GSLT is only necessary if you want the server to “own” a Steam account for features such as:

* **Server-owned inventory or workshop rights** (e.g. publishing mods directly from server).
* **Tying a specific Steam user account** to your server instance for centralised control or auditing.

If you decide to use a GSLT:

* It must be generated in your Steamworks partner dashboard (Steam Community → Game Server Account Management) [steamcommunity.com](https://steamcommunity.com/dev/managegameservers?utm_source=chatgpt.com).
* Each token is linked to a single App ID.
* A GSLT can only be used by one server process at a time—if a second server logs in with the same token, the first will be kicked off.
* Tokens expire if unused for a long period; you can regenerate or revoke them via the same management page [steamcommunity.com](https://steamcommunity.com/dev/managegameservers?utm_source=chatgpt.com).
* There’s a per-account limit (currently 1,000 tokens) and account requirements (e.g. phone verified, not community-banned, must own the App ID) [steamcommunity.com](https://steamcommunity.com/dev/managegameservers?utm_source=chatgpt.com).

In most cases, you simply:

1. Reference your App ID in `steam_appid.txt` or via code.
2. Call `SteamGameServer.Init(...)`.
3. Call `SteamGameServer.LogOnAnonymous()`.
4. Call `SteamGameServer.SetAdvertiseServerActive(true)` (and set a server name).

This flow gives you full browser listing, VAC support, player counts, and telemetry. Adding a GSLT is only for advanced scenarios where you need server-account ownership or specific workflow control. If you don’t have those requirements, you can omit GSLT entirely.

### Relationship with Steamworks SDK Redist

Steam Game Servers depend on Valve’s **Steamworks SDK Redistributable** (App ID 1007) for the low‐level libraries that interface with Steam’s backend. These include, for example:

* `steamclient64.dll` / `steamclient.so`
* `tier0_s64.dll` / `tier0_s64.so`
* `vstdlib_s64.dll` / `vstdlib_s64.so`
* `steam_api64.dll` / `steam_api.so`

**Pulling Dependencies via SteamCMD**

Rather than bundling these files manually, you can let **SteamCMD** fetch them on your server at deploy time. On Windows or Linux:

```
steamcmd +login anonymous \
        +force_install_dir /path/to/sdk_files \
        +app_update 1007 validate \
        +quit
```

This ensures you always get the correct platform ABI (x64 vs. x86) and version. Place the resulting `.dll`/`.so` files alongside your server executable so the Steam API will load them at runtime.

**Pulling Your Server Build via SteamCMD**

You can also use SteamCMD to pull down your own server application (once it’s published to a depot). For example:

```
steamcmd +login anonymous \
        +force_install_dir /path/to/server_build \
        +app_update <YourServerAppID> validate \
        +quit
```

This approach makes deploying or updating a server much easier—just rerun SteamCMD on the target machine and it will download only the changed files.

> **Tip:** If you use a managed backend service (PlayFab, GameLift, GPortal, etc.), they often include automatic SteamCMD integration. In those cases, manually running SteamCMD for dependencies or builds is usually redundant—your hosting provider handles it for you.

## Steam Game Server Lifecycle

Below is an overview of the main phases a Steam Game Server goes through. While engines like Unreal (via Steam Shared) or Unity (using Heathen’s Toolkit) automate most of these steps, it’s helpful to understand what happens behind the curtain.

### Initialisation

* **What Happens**:\
  The server process loads the Steam Game Server libraries and establishes a connection to Steam’s backend. This tells Valve that “this process is a game server for App ID XYZ” and reserves the ports you’ve chosen for gameplay and queries.
* **Behind the Scenes**:
  * The Steam API checks for the correct redistributable binaries (steamclient, tier0, steam\_api, etc.).
  * A lightweight handshake occurs with Valve’s servers to validate your App ID and ensure those binaries are compatible.
  * Once initialised, the server is ready to accept further configuration settings.

### Configuration

* **What Happens**:\
  Before “going live,” you supply metadata about your server—things like maximum player count, map name, whether it’s password-protected, and the human-readable server name.
* **Behind the Scenes**:
  * These values are stored locally until the server logs on.
  * When you later advertise the server, Steam’s master servers will index this metadata so clients can filter and sort by player count, map, or other attributes.

### LogOn / LogOff

* **LogOn (Connecting to Steam Matchmaking)**:
  * **Anonymous Login**: By default, modern Steamworks servers use anonymous login. You do not need a Game Server Login Token (GSLT) just to appear publicly—once you log on anonymously, you are treated as a valid host for listing, VAC, player counts, etc.
  * **Authenticated (GSLT) Login**: If you need to “own” the server under a specific Steam account (for workshop publishing, inventory management, or tighter control), you provide a GSLT issued from your Steamworks dashboard. Functionally, both login methods yield the same public visibility—choosing GSLT is only necessary for account-linked workflows.
* **LogOff (Graceful Disconnect)**:
  * When you want to stop listing or shut down, you tell Steam to log off. This immediately removes your server from the public index and closes matchmaking connections. The server can later log on again if needed.

### Heartbeats and Visibility

* **Automatic Heartbeats**:
  * After a successful logon, the Steam backend expects a periodic “I’m alive” signal (a heartbeat). By default, the Steam API handles this internally (approximately every 2 minutes), refreshing your server’s metadata (players, map, etc.) in the master list.
  * If heartbeats stop—for example, if your process hangs or loses connection—Steam will automatically delist your server.
* **Pumping Callbacks**:
  * While heartbeats are internal, your server still needs to regularly process Steam events (matchmaking queries, authentication results, etc.). In Unity/Heathen or Unreal/Steam Shared, this is wired into the engine’s update loop. Behind the scenes, these callbacks ensure that incoming player join requests or query packets are handled promptly.
* **Dynamic Updates**:
  * If you change metadata at runtime (e.g. current player count or map name), those updated values are picked up on the next heartbeat, so clients see the latest info in the server browser.

### Shutdown and Cleanup

* **LogOff**:
  * First, you notify Steam that the server is going offline—this removes it from the browser instantly.
* **Library Shutdown**:
  * Next, the Steam API tears down its connections, stops any background threads, and releases memory associated with the Steam Game Server libraries.
  * In most high-level toolkits (Heathen, Unreal’s Steam Shared), this is triggered when your server application exits, so no manual intervention is needed.
* **Process Exit**:
  * Once Steam has been cleanly shut down, the server process terminates.
  * If you restart the process later, the cycle begins again with initialisation.

**Summary**: Even though modern engines and toolkits handle most of the grunt work—automatically linking against Steam’s server libraries, updating metadata, and maintaining heartbeats—the server lifecycle still follows these core phases. Understanding them helps when diagnosing why a server might not appear in the browser, why it might get delisted, or why certain configuration values aren’t being picked up.

***

## Building and Running a Steam Game Server

Whether you are new to Steam Game Servers or a seasoned developer, there are a few key considerations to ensure your server build works reliably across platforms. Below is a concise guide to headless builds, dependencies, and configuration files. Examples for Unity, Unreal, and Steamworks .NET are marked where appropriate.

***

### General Build Considerations

1. **Headless / Server-Only Builds**
   * A “headless” or dedicated server build runs without a graphical user interface.
   * Engines often provide a specific build target for servers:
     * **Unity**: Use the built-in “Dedicated Server” or set the `UNITY_SERVER` compilation flag.
       * _Example: Unity configuration goes here._
     * **Unreal**: Select the “Server” target when packaging. Steam integration is handled by Unreal’s Steam Shared module.
       * _Example: Unreal packaging steps go here._
     * **Steamworks .NET (Custom Engines)**: Compile a separate server executable that links against the Steam Game Server libraries rather than the client libraries.
       * _Example: Steamworks .NET project setup goes here._
2. **Server-Specific Compilation Flags**
   * Most engines conditionally compile Steam Game Server code when a “server” flag is defined.
     * In Unity, `UNITY_SERVER` switches from `SteamClient` to `SteamGameServer` interfaces.
     * In custom builds, ensure you include and invoke `ISteamGameServer` rather than `ISteamClient`.
   * Verify your build settings to confirm the correct libraries are referenced for a headless environment.
3. **Including Required `.dll` / `.so` Dependencies**
   * The server binary must be accompanied by Steam’s redistributable libraries, matching platform and architecture (e.g. x64 vs x86).
   * On Windows, these are named like `steam_api64.dll`, `steamclient64.dll`, `tier0_s64.dll`, `vstdlib_s64.dll`.
   * On Linux, they appear as `.so` libraries (e.g. `libsteam_api.so`, `libsteamclient.so`).
   * Place these libraries in the same folder as your server executable so the loader can find them at runtime.
4. **`steam_appid.txt` Placement and Use**
   * A simple text file named `steam_appid.txt`, containing only your App ID, should sit next to the server executable in the build’s root directory.
   * This file allows Steam’s API to validate which game is being hosted without requiring recompilation.
   * In CI or automated pipelines, ensure `steam_appid.txt` is copied into the output directory before deployment.
5. **When to Use App ID 1007 (Steamworks SDK Redist)**
   * App ID 1007 is Valve’s **Steamworks SDK Redistributable**. It provides all necessary runtime libraries for Steam Game Servers.
   * Use App ID 1007 if you prefer not to bundle libraries manually. SteamCMD (or SteamPipe) can fetch them directly on your server at deploy time.
   * If you include App ID 1007 in your depot, end users (or your hosting infrastructure) can pull dependencies simply by referencing that App ID during an update.

***

### Dependencies

**List of Required Runtime Binaries (Per Platform)**

* **Windows (x64)**:
  * `steam_api64.dll`
  * `steamclient64.dll`
  * `tier0_s64.dll`
  * `vstdlib_s64.dll`
* **Windows (x86)** (if still supported for older engines):
  * `steam_api.dll`
  * `steamclient.dll`
  * `tier0_s.dll`
  * `vstdlib_s.dll`
* **Linux (x64)**:
  * `libsteam_api.so`
  * `libsteamclient.so`
  * `libtier0_s64.so`
  * `libvstdlib_s64.so`

> **Tip for macOS**: While less common for game servers, macOS builds use `.dylib` versions. Ensure compatibility flags if supporting Mac.

**Methods to Obtain Dependencies**

App ID **1007** is used **only to download the Steamworks redistributable binaries via `steamcmd`**. It **should not** be linked to your own App ID or listed as a dependency in your depot — Steam does **not** support declaring App ID 1007 as a "Common Redistributable" or dependency for SteamPipe builds.

Use App ID 1007 when:

* You want to pull the required Steam runtime libraries onto a remote server.
* You're managing dedicated server environments via script or automation.

**Example usage:**

```bash
steamcmd +login anonymous \
         +force_install_dir ./steamworks_redist \
         +app_update 1007 validate \
         +quit
```

This will install the redistributable binaries to the given directory. These can then be copied or symlinked into your server's runtime folder.

> **Note**: If you use a managed hosting provider (e.g., PlayFab, GameLift, GPortal), they often offer built-in SteamCMD integrations. In those environments, you typically only need to specify your Game App ID and depot details; the provider fetches dependencies and deploys your server automatically, making manual SteamCMD steps redundant.

***

## Server Discovery via Steam Game Server Browser

The **Steam Game Server Browser (SGSB)** enables clients to discover internet-accessible and local (LAN) servers running your game. Discovery relies on querying the Steam backend or broadcasting over LAN.

### How Discovery Works

Discovery queries can originate from multiple sources:

* **Internet** – Returns public, VAC-secured or unsecured dedicated servers.
* **LAN** – Uses broadcast discovery within the local subnet.
* **Favorites** – User-curated list of servers marked as favorites.
* **Friends** – Servers where friends are currently playing.
* **History** – Previously joined servers.

These discovery categories correspond to filters in the Steam client’s built-in server browser and are available to games using the Steam APIs.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not entirely possible as your UI to display the results will be up to you and likely will require some coding, the act of querying for servers, however, is trivial and can be done code-free.

<figure><img src="../.gitbook/assets/image (366).png" alt=""><figcaption></figcaption></figure>

The Game Server Browser Manager provides an easy-to-use component you can call to get various lists of servers and it will raise an event when the search is completed that contains the results. You can then connect that to your own UI, however you see fit to display those results.

You can call to get a list with no code via Unity Events, such as a button's Click event.

<figure><img src="../.gitbook/assets/image (367).png" alt=""><figcaption></figcaption></figure>

Or you can call it from code just as easily:

```csharp
gameServerBrowserManager.GetAllInternet();
```

## C\#

The Matchmaking API includes a number of helper functions all of which take the same argument list.

```csharp
AppId_t appId,
MatchMakingKeyValuePair_t[] filters, 
ISteamMatchmakingServerListResponse pRequestServersResponse
```

The funcitons are as follows:

```csharp
API.Matchmaking.Client.RequestFavoritesServerList
API.Matchmaking.Client.RequestFriendsServerList
API.Matchmaking.Client.RequestHistoryServerList
API.Matchmaking.Client.RequestInternetServerList
API.Matchmaking.Client.RequestLANServerList
API.Matchmaking.Client.RequestSpectatorServerList
```

For example

```csharp
API.Matchmaking.Client.RequestInternetServerList(appId, filters, m_ServerListResponse)
```

As far as creating the `MatchMakingKeyValuePair_t` :&#x20;

```csharp
var array = new MatchMakingKeyValuePair_t[Count];
int index = 0;
foreach (var pair in this)
{
    array[index] = new MatchMakingKeyValuePair_t() { m_szKey = pair.Key, m_szValue = pair.Value };
    index++;
}
```

The `ISteamMatchmakingServerListResponse` is next:

```csharp
m_ServerListResponse = new ISteamMatchmakingServerListResponse(OnServerResponded, OnServerFailedToRespond, OnRefreshComplete);
```

Where

```csharp
private void OnServerResponded(HServerListRequest hRequest, int iServer)
{
    Debug.Log("OnServerResponded: " + hRequest + " - " + iServer);
}

private void OnServerFailedToRespond(HServerListRequest hRequest, int iServer)
{
    Debug.Log("OnServerFailedToRespond: " + hRequest + " - " + iServer);
}

private void OnRefreshComplete(HServerListRequest hRequest, EMatchMakingServerResponse response)
{
    Debug.Log("OnRefreshComplete: " + hRequest + " - " + response);
    List<GameServerBrowserEntry> serverResults = new();
    var count = SteamMatchmakingServers.GetServerCount(hRequest);

    for (int i = 0; i < count; i++)
    {
        var serverItem = SteamMatchmakingServers.GetServerDetails(hRequest, i);

        if (serverItem.m_steamID.m_SteamID != 0 && serverItem.m_nAppID == API.App.Id)
        {
            GameServerBrowserEntry entry = new GameServerBrowserEntry(serverItem);
            serverResults.Add(entry);
        }
    }

    if (hRequest != HServerListRequest.Invalid)
    {
        SteamMatchmakingServers.ReleaseRequest(hRequest);
    }

    // Do something with serverResults
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

You can request

* Favorite
* LAN
* Internet
* Friends
* Spectator

Server lists, each call takes a filter and App ID input and invokes an event when complete, the event will contain an array of Game Server Item Wrappers, which each contains detailed information about each server found.

<figure><img src="../.gitbook/assets/image (368).png" alt=""><figcaption></figcaption></figure>

## C++

Lets create a helper class ... Heathen calls these "linkers" and they make linking native Steamworks calls to Unreal objects easier.

```cpp
class SteamMatchmakingServerListResponseLinker : public ISteamMatchmakingServerListResponse
{
public:
    HServerListRequest listHandle;

    SteamMatchmakingServerListResponseLinker(FSteamServerListResponce InCallback);
    virtual ~SteamMatchmakingServerListResponseLinker();

    // Server has responded ok with updated data
    void ServerResponded(HServerListRequest hRequest, int iServer);
    // Server has failed to respond
    void ServerFailedToRespond(HServerListRequest hRequest, int iServer);
    // A list refresh you had initiated is now 100% completed
    void RefreshComplete(HServerListRequest hRequest, EMatchMakingServerResponse response);

private:
    FSteamServerListResponce Callback;
    TArray<FGameServerItemWrapper> results;
};
```

So as you can see the linker's constructor expects an `FSteamServerListResponce` delegate; here is how we defined that.

```cpp
DECLARE_DYNAMIC_DELEGATE_OneParam(FSteamServerListResponce, const TArray<FGameServerItemWrapper>&, servers);
```

The idea is simple: you create this delegate, pass it into the Linker's constructor, and the linker will handle the native callbacks for you and pack that down into an Unreal-style delegate. This can be easily exposed to your designers in Blueprint or used directly in C++

The below code is from our Toolkit's Blueprint library, its assuming the filters come in as

```cpp
USTRUCT(BlueprintType)
struct FKeyValuePair
{
    GENERATED_BODY()

public:
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Heathen's Toolkit|Steamworks")
        FString Key;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Heathen's Toolkit|Steamworks")
        FString Value;
};
```

The body of the `UFUNCTION(BlueprintCallable)` is then

```cpp
TArray<MatchMakingKeyValuePair_t> pFilter;
pFilter.Reserve(filter.Num());
for (int i = 0; i < filter.Num(); i++)
{
	MatchMakingKeyValuePair_t nEntry(StringCast<ANSICHAR>(*filter[i].Key).Get(), StringCast<ANSICHAR>(*filter[i].Value).Get());
	pFilter.Add(nEntry);
}

// Get a pointer to the data in the vector
MatchMakingKeyValuePair_t* pFilterArray = pFilter.GetData();
uint32 nFilters = pFilter.Num();

SteamMatchmakingServerListResponseLinker* linker = new SteamMatchmakingServerListResponseLinker(callback);
linker->listHandle = SteamMatchmakingServers()->RequestInternetServerList(static_cast<AppId_t>(appId), &pFilterArray, nFilters, linker);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

***

### Use Cases and Implementation Guidance

Key implementation guidance:

* **Asynchronous**: Discovery queries are non-blocking and deliver results via callbacks.
* **Query Rate Limits**: Steam imposes limits to avoid abuse. Queue large queries or paginate.
* **Connection Strategy**: Use the Steam-provided IP:port to establish direct connection or authenticate via Steam Networking.
* **Fallback**: For LAN-only or offline modes, broadcast-based discovery should be used.

***

### Handling Responses

SteamMatchmakingServers supports three types of detailed queries per server:

1. **Ping** (`PingServer`)\
   Measures latency and retrieves basic server info (IP, name, players, etc.)
2. **Rules** (`ServerRules`)\
   Returns key-value pairs of game-defined server rules/settings.
3. **Players** (`PlayerDetails`)\
   Returns a list of connected players and their metadata (name, score, time connected).

Responses are returned via associated callback interfaces and may fail or timeout. Always implement retry logic and handle dropped or malformed responses.

***

## IT Ops: Hosting & Deployment

Below is an engine‐agnostic overview of hosting options and CI/CD practices for Steam Game Servers. All statements are grounded in official documentation or widely accepted best practices.

***

### Hosting Options

**Self-Hosted**

Running your own hardware or virtual machines gives you full control but comes with specific requirements:

1. **Bandwidth and Uptime**
   * **Bandwidth**: Ensure sufficient upstream bandwidth for expected player concurrency. Each client connection uses both upload and download.
   * **Uptime**: A reliable, always-on connection is critical. Downtime causes your server to drop out of Steam’s master server list when heartbeats stop.
2. **Ports and Firewall**
   * **Game Port**: By default, many Steam Game Servers use **27015** (UDP/TCP) for game traffic, but you must configure this explicitly.
   * **Query Port**: The server also opens a separate query port (commonly **27016**).
   * **Firewall Rules**: Open both ports in your OS firewall and any upstream network firewall. Steam’s master servers must be able to reach your query port to index your server [partner.steamgames.com](https://partner.steamgames.com/doc/sdk/uploading/distributing_gs).
3. **Static IP or DNS**
   * Using a **static public IP** (or a DNS name pointing to it) ensures clients can reliably connect. Dynamic DNS can work, but frequent IP changes may cause delisting or confusion in connection attempts.
4. **SteamCMD Deployment**
   *   Steam Game Server binaries (App ID 1007) and your own server build (your dedicated Server App ID) must both be pulled via SteamCMD. For example:

       ```
       steamcmd +login anonymous 
               +force_install_dir /opt/steam_redist 
               +app_update 1007 validate 
               +quit
       steamcmd +login anonymous 
               +force_install_dir /opt/my_game_server 
               +app_update <YourServerAppID> validate 
               +quit
       ```

       This ensures you have the correct Steamworks runtime libraries and the latest server build [partner.steamgames.com](https://partner.steamgames.com/doc/sdk/uploading/distributing_gs).
5. **Deployment Strategies**
   * **Systemd (Linux)**: Create a `.service` unit that starts your server executable, automatically restarts on failure, and logs stdout/stderr to the system journal.
   * **Windows Service**: Use a tool like NSSM or Windows Server Resource Kit to wrap your server executable as a native Windows service.
   * **Docker Containers**: Containerise your server with a minimal base image (e.g. Ubuntu Server). Use a `Dockerfile` that runs `steamcmd` at build or runtime, then launches the server in headless mode. Configure `restart: always` in your `docker-compose.yml` or Kubernetes Pod spec.

> **Tip:** Steamworks documentation notes that when you release a dedicated server in Steamworks, your server App ID is automatically added to SteamCMD’s anonymous package (pkg 17906), making it publicly downloadable via SteamCMD without requiring login [partner.steamgames.com](https://partner.steamgames.com/doc/sdk/uploading/distributing_gs).

***

**Managed Hosting**

Several companies specialise in renting game server instances, automating SteamCMD downloads, and providing dashboards for server management:

* **GPortal**
* **GameServers.com**
* **Nodecraft**
* **Multiplay (Unity)**
* **OVH Game Servers**

**Common features**:

* Automated SteamCMD integration (no manual `steamcmd` steps).
* Web-based control panels for starting/stopping servers, viewing logs, and managing configuration files.
* Built-in DDoS protection and global data center presence to minimise latency.
* Billing models based on slot count or instance size.

Because these providers handle SteamCMD and OS-level configuration behind the scenes, you typically only need to upload your server build (via their panel or an automated FTP/SFTP process). Consult each provider’s documentation for specifics.

***

**Platform-Integrated Services**

**PlayFab Multiplayer Servers (Azure PlayFab)**

* **Overview**: PlayFab Multiplayer Servers let you upload, deploy, and orchestrate game server builds within Azure data centers. It integrates matchmaking, scaling, and health monitoring.
* **Key resources**:
  * “Deploying PlayFab multiplayer server builds” guides you through packaging your server and uploading it to PlayFab [learn.microsoft.com](https://learn.microsoft.com/en-us/gaming/playfab/multiplayer/).
  * PlayFab’s GSDK (Game Server SDK) handles lifecycle events (OnStart, OnStop) and communicates with PlayFab for health checks and session allocation.
* **Advantages**:
  * Pay-as-you-go compute resources.
  * Automatic scaling based on queue metrics.
  * Built-in telemetry and logging.
  * Integrated matchmaking via PlayFab Party or custom solutions.

**AWS GameLift**

* **Overview**: Amazon GameLift is a fully managed dedicated server hosting service. You define your server build, upload it to an S3 bucket, and GameLift runs fleets of instances in regions you choose.
* **Key resources**:
  * “Amazon GameLift Integration Guide for Custom Game Servers” explains how to configure your Linux/Windows build alongside GameLift’s Server SDK [aws.amazon.com](https://aws.amazon.com/gamelift/gamelift-resources-gamelift-feature/).
  * GameLift Fleets handle auto-scaling, health checks, and match backfilling.
* **Advantages**:
  * Low-latency regional deployment across AWS’s global infrastructure.
  * Cost management via spot instances or on-demand.
  * Flexible fleet autoscaling policies.
  * Integrated QoS (Quality-of-Service) beacons for latency-based matchmaking.

**Azure PlayFab Containers**

* **Overview**: A more recent offering where you deploy PlayFab server builds as containerised workloads on Azure Kubernetes Service (AKS).
* **Key resources**:
  * “PlayFab Multiplayer Servers” documentation covers deploying Docker images to container-based hosting on Azure [learn.microsoft.com](https://learn.microsoft.com/en-us/gaming/playfab/multiplayer/).
* **Advantages**:
  * Full Kubernetes feature set for orchestration (rolling updates, self-healing).
  * Leverage AKS’s autoscaling and regional distribution.
  * Integrates with Azure monitoring and logging.

***

## CI/CD and Automation

A robust CI/CD pipeline ensures that server builds are tested, packaged, and deployed with minimal manual intervention.

**Using SteamPipe for Server Builds**

1. **Build and Upload**
   * On build servers (e.g., Jenkins, GitHub Actions, Azure Pipelines), compile your server in “server” mode (headless).
   * Create or update your **depot manifest** (`depot_build.vdf`) to include:
     * All server binaries and configuration files.
     * A `steam_appid.txt` file containing your App ID.
   *   Run **ContentBuilder** to upload to SteamPipe:

       ```
       ContentBuilder.exe +login <steam_user> <password> \
                         +run_app_build <path_to_depot_build.vdf> \
                         +quit
       ```
   * After uploading, use the Steamworks **Builds** page to create or update branches (for example, “default”, “staging”, “experimental”) [partner.steamgames.com](https://partner.steamgames.com/doc/store/application/builds)
2. **Branch Management**
   * Steamworks allows multiple branches (Betas) so you can test “staging” builds before promoting them to “default” for public use.
   * Use naming conventions like `release-v1.2.3` or `qc-build` and assign passphrases if you want password-protected access [partner.steamgames.com](https://partner.steamgames.com/doc/store/application/branches).

***

**Pulling Dependencies During CI with SteamCMD**

* **Steamworks Redistributables (App 1007)**
  *   Before packaging your build, fetch the latest Steamworks SDK Redistributable via SteamCMD on your build agent:

      ```
      steamcmd +login anonymous \
              +force_install_dir ./steamworks_redist \
              +app_update 1007 validate \
              +quit
      ```
  * Copy the resulting binaries into your server build’s output folder so that SteamPipe packages them alongside your server executable [partner.steamgames.com](https://partner.steamgames.com/doc/sdk/uploading/distributing_gs).
* **Your Server Build**
  *   After uploading your server binaries to a depot (with SteamPipe), you can pull them to a QA or staging server automatically in your CI pipeline:

      ```
      steamcmd +login anonymous \
              +force_install_dir ./deployed_server \
              +app_update <YourServerAppID> -beta <branch_name> validate \
              +quit
      ```
  * Use this step to provision test servers, run integration tests, or validate that the new build successfully logs onto Steam.

***

**Monitoring and Auto-Restart**

* **Process Supervision**
  * **Linux**:
    * Use a **systemd** unit file with `Restart=on-failure` (or `always`) so the server automatically restarts if it crashes.
    *   Example snippet:

        ```ini
        [Service]
        ExecStart=/opt/my_server/MyServerExecutable
        Restart=on-failure
        RestartSec=5
        WorkingDirectory=/opt/my_server
        StandardOutput=syslog
        StandardError=syslog
        ```
  * **Windows**:
    * Wrap your server in a Windows Service (e.g., using NSSM). Configure the service to **restart on failure** in the service Recovery options.
* **Health Checks and Alerts**
  * Implement periodic heartbeats in your server monitoring system: check that the process is still running, responding on the query port, and appearing in Steam’s master list.
  * Use tools like **Prometheus + Grafana**, **Datadog**, or **Azure Monitor** to collect metrics (CPU, memory, player count) and set alerts on anomalies (e.g., CPU spike, player-count drop, server offline).
* **Containerized Restarts**
  * If you run in Docker or Kubernetes, set `restart: always` (Docker Compose) or a Kubernetes **Deployment** with `livenessProbe` and `readinessProbe`. When probes fail, the orchestrator automatically restarts the pod.

***

**Summary**:

* **Self-hosting** gives maximum control but requires managing SteamCMD, ports, firewalls, and uptime.
* **Managed hosting** services automate much of the deployment, billing, and DDoS protection.
* **Platform-integrated services** (PlayFab, GameLift, Azure) add autoscaling, matchmaking integration, and health monitoring at the cost of additional platform dependency.
* A solid CI/CD pipeline should use **SteamPipe** for uploading builds, **SteamCMD** for fetching redistributables, and standard process supervisors (systemd, Windows Services, Docker/Kubernetes) for automatic restarts and health checks.

***

## Troubleshooting

Below are common issues encountered when setting up Steam Game Servers, along with guidance on diagnosing and resolving them. All advice is grounded in official Steamworks documentation and community-verified experiences.

### Common Causes of Invisible Servers

1. **Server Not Advertising Properly**\
   If you never call the equivalent of `SetAdvertiseServerActive(true)` (or your engine/toolkit’s wrapper), Steam’s master servers will not list your server—even if it’s otherwise fully initialized. Ensure that:
   * You have set a non-empty server name.
   * You explicitly enable advertising after a successful logon.\
     [partner.steamgames.com](https://partner.steamgames.com/doc/features/multiplayer/game_servers).
2. **Missing or Incorrect Server Name**\
   Steam treats a blank name as “do not list.” Double-check that your server configuration supplies a valid, human-readable name before advertising.
3. **Port or Firewall Blockage**
   * **Game Port vs. Query Port**: Steam Game Servers typically use two ports (e.g., default 27015 for gameplay and 27016 for queries). If either is blocked, Steam cannot verify that your server is alive or respond to listing requests.
   * **Firewall Rules**: Confirm that both UDP and TCP are open on those ports (Steam uses UDP for heartbeats and game traffic; TCP may be needed for RCON or certain query types). Disabling your firewall temporarily, adding a specific rule, or testing on a LAN can help isolate issues [partner.steamgames.com](https://partner.steamgames.com/doc/features/multiplayer/game_servers)
4. **NAT, Loopback, or Public IP Misconfiguration**
   * If your server is behind a NAT, incoming Steam queries may not reach it unless you forward the correct ports on your router.
   * To test local discovery, check the “LAN” tab in the Steam Server Browser. If the server appears there but not under “Internet,” network address translation or ISP-level filtering may be preventing public listing [steamcommunity.com](https://steamcommunity.com/app/573090/discussions/0/4357871761805093964/).
   * Some ISPs block or shape certain UDP ports; test at different times and contact your ISP if necessary [help.steampowered.com](https://help.steampowered.com/en/faqs/view/669A-2F68-D1D1-A5EC).
5. **Incorrect Universe or App ID**
   * Ensure you initialize using the correct “Universe” (typically `k_EUniversePublic`) so Steam knows to list you on the public master servers rather than a QA or Dev environment.
   * Verify that `steam_appid.txt` matches your published App ID exactly. A typo here can cause Steam to reject heartbeats silently.
6. **Wrong “ModDir” or Game Directory String**
   * Valve uses the “Mod Directory” string (e.g., `"spacewar"` for the sample) as part of server listing filters. If you use a custom ModDir that isn’t recognized by Steam’s backend, your server may fail to appear in Internet listings even if it shows under LAN or “Favorites.”\
     [github.com](https://github.com/Facepunch/Facepunch.Steamworks/issues/22).

***

### Server Not Logging On

1. **Missing `steam_appid.txt`**
   * When running a server outside the Steam client, Steam’s API expects to find a plain text file named `steam_appid.txt` (containing only your App ID). If that file is absent or contains the wrong App ID, initialization fails silently.
   * Place `steam_appid.txt` in the same directory as your server executable and confirm the contents match your Steamworks App ID.
2. **Unavailable or Outdated Steamworks Redistributable**
   * If the required runtime libraries (`steam_api64.dll`, `steamclient64.dll`, etc., on Windows; `.so` files on Linux) are missing or mismatched, the server cannot initialize the Steam Game Server API.
   * Use SteamCMD to pull App 1007 (Steamworks SDK Redistributable) onto your build or server machine before launching [github.com](https://github.com/rlabrecque/Steamworks.NET/issues/250).
3. **GSLT (Game Server Login Token) Issues**
   * If you choose to use an authenticated login via a GSLT, ensure that:
     * The token is valid for your App ID.
     * No other server process is currently using the same token (each GSLT can only be active on one process at a time).
   * If anonymous login (`LogOnAnonymous`) is preferable, remove any `LogOn(token)` calls. Modern Steamworks treats anonymous login as fully capable of listing, authentication, and VAC integration [github.com](https://github.com/rlabrecque/Steamworks.NET/issues/250).
4. **Network Connectivity**
   *   Confirm that the server machine can reach Steam’s backend. On Linux, run:

       ```bash
       telnet support.steampowered.com 80
       ```

       or check DNS resolution.
   * Look for errors like `GameServer.LogOn timed out` in your console or logs, which often indicate that the server cannot reach the Steam authentication servers [steamcommunity.com](https://steamcommunity.com/app/251570/discussions/1/3190241555982307105/).
5. **Steam Service Not Running (Windows)**
   * On Windows, Steam’s “Steam Client Service” (or older “SteamService”) must be running when launching a dedicated server that uses the SteamPipe UI.
   * If you installed SteamCMD manually, ensure it has successfully updated and that no residual Steam client dialogs are blocking the process.

***

### Port Conflicts and Firewall Issues

1. **Identifying Port Usage**
   * Use OS utilities (e.g., `netstat -an | grep 27015` on Linux or `netstat -ab` on Windows) to verify that your chosen UDP/TCP ports are free before you start the server.
   * If another process (e.g., another game server or a different service) is already bound to those ports, choose alternate ports in your configuration and forward them accordingly.
2. **Firewall Configuration**
   * On **Windows**, add inbound and outbound rules in **Windows Defender Firewall** to allow UDP traffic on both the game port and query port.
   *   On **Linux**, use `ufw` or `iptables` to open UDP ports:

       ```bash
       sudo ufw allow 27015/udp
       sudo ufw allow 27016/udp
       ```
   * Some router firewalls require manual port forwarding: forward the same ports to your server’s local IP address. Confirm both TCP and UDP as needed; though Steam primarily uses UDP, certain query functions may use TCP [steamcommunity.com](https://steamcommunity.com/app/573090/discussions/0/4357871761805093964/).
3. **ISP-Level Blocking**
   * If no local firewall is blocking but your server still fails to respond to the Steam master servers, test from a different network or ask friends in different regions to attempt to add your server by IP. Some ISPs throttle or block non-standard UDP traffic during peak hours [help.steampowered.com](https://help.steampowered.com/en/faqs/view/669A-2F68-D1D1-A5EC).
4. **NAT Loopback Testing**
   * To verify that port forwarding is correctly configured, attempt to add the server in Steam’s “LAN” tab (using a local IP) and then from “Favorites” (using your public IP). If LAN discovery works but the public listing does not, your NAT or ISP is the likely culprit [steamcommunity.com](https://steamcommunity.com/app/573090/discussions/0/4357871761805093964/)

***

### Debug Logging and Validation

1. **Enabling Steamworks Debug Logs**
   * **Windows**:
     * Add `-console` and `-log` arguments to your dedicated server launch command (if supported by your build), or set the environment variable `SteamAppId=<YourAppID>`.
     * Check `%ProgramFiles(x86)%\Steam\logs\` (e.g., `content_log.txt`, `connection_log.txt`) for error messages relating to game server initialization or heartbeats.
   * **Linux**:
     * Run your server with `STEAM_LOG=1 ./MyServer` (if using SteamCMD), then check `~/.steam/error.log` or `~/.local/share/Steam/logs/` for similar entries.
2. **Verifying Heartbeats and Listings**
   * Use the CLI tool `masterserver query` or a third-party web interface (e.g., Steam Server Browser websites) to confirm that Steam’s master servers acknowledge your heartbeat.
   *   Look for a message like:

       ```
       [GameServer] Sent heartbeat to master servers; response: OK
       ```
   * If you see “FailedToRespond” or similar errors, investigate network connectivity [github.com](https://github.com/rlabrecque/Steamworks.NET/issues/250).
3. **Testing Individual Server Queries**
   * After confirming a server is running, use `PingServer(IP, port)` and `ServerRules(IP, port)` (via SteamMatchmakingServers) to retrieve basic paddle data. If these calls succeed but the server still doesn’t appear in the master list, the issue likely lies in advertising or configuration rather than raw network reachability [partner.steamgames.com](https://partner.steamgames.com/doc/features/multiplayer/game_servers).
4. **Common Log Messages**
   * `GameServer.Init failed`: Usually indicates missing or incompatible redistributable libraries or incorrect `steam_appid.txt`.
   * `GameServer.LogOn timed out`: Network connectivity problem or Steam backend unreachable; check firewall and ISP.
   * `GameServer.LogOnDenied_VerifyAccountLocked`: The Steam account associated with a GSLT is locked or doesn’t own the game. Switch to anonymous login if you don’t need a GSLT [steamcommunity.com](https://steamcommunity.com/app/251570/discussions/1/3190241555982307105/).

***

## FAQ

**Q1: Why does my server show up under LAN but not Internet?**

* Answer: LAN discovery bypasses Steam’s master servers entirely and simply broadcasts on your local subnet. If LAN works but Internet does not, confirm that:
  1. Your public IP is forwarded to the correct internal IP.
  2. UDP ports are open in both OS and router firewalls.
  3. Your ISP is not blocking or NAT-loopbacking UDP traffic [steamcommunity.com](https://steamcommunity.com/app/573090/discussions/0/4357871761805093964/)

**Q2: My server is “unresponsive” or “FailedToRespond” in the Steam Server Browser. What now?**

* Answer: This indicates that Steam’s master servers see your IP:port but cannot get a valid response within the timeout window. Verify that:
  1. The server process is still running and pumping Steam callbacks.
  2. The query port matches what you configured in both your code and your firewall/router.
  3. No other process is bound to that port (use `netstat` to confirm) [github.com](https://github.com/rlabrecque/Steamworks.NET/issues/250).

**Q3: Does my server need a GSLT if I only want public listing?**

* Answer: No. Modern Steamworks allows **anonymous logon** (`LogOnAnonymous()`) and full public listing (including VAC protection) without a GSLT. Only use a GSLT if you need server-account ownership (e.g., workshop publishing) or want to track a specific Steam account.

**Q4: Why do I get “LogOnDenied\_GameServerInitFailed” ?**

* Answer: This means the Steam Game Server API failed to initialize. Common causes:
  1. `steam_appid.txt` is missing or contains an incorrect App ID.
  2. Required redistributable binaries (App 1007) are missing or on the wrong path.
  3. Insufficient permissions or user account conflicts (e.g., running SteamCMD as a different user than your server process). Refer to Valve’s “Distributing Your Dedicated Game Server” docs [partner.steamgames.com](https://partner.steamgames.com/doc/features/multiplayer/game_servers).

**Q5: How do I force my server to refresh its listing metadata (map name, player count) without restarting?**

* Answer: Call the appropriate `Set*` methods again (e.g., `SetMapName`, `SetMaxPlayerCount`) between heartbeats. Steam’s next automatic heartbeat (approx. every 2 minutes) will reflect these new values in the master list. Alternatively, you may force a manual “heartbeat” reload by briefly toggling advertising off and on.
