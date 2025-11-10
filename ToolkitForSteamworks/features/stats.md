# Stats

Steam Stats are numeric values you can store for the user against your game, these can be "client" or "GS" meaning Game Server based. Here we will summarise the key information you should have already read in [Valve's Stats and Achievements article](https://partner.steamgames.com/doc/features/achievements) 😉

## Types and Configuration

Stats come in 4 types

* Int\
  A simple whole number
* Float\
  A (decimal) number such as 1.25&#x20;
* AVGRATE\
  A moving average, e.g. average among users over the past 2 weeks, etc.

Each stat has the following configuration values

* **ID** \
  An automatically-generated numerical ID for each stat.
* **Type** \
  The type of this Stat - INT, FLOAT, or [AVGRATE](https://partner.steamgames.com/doc/features/achievements#AVGRATE).
* **API Name** \
  The string used to access this stat using the API.
* **Set By** \
  Sets who can modify the stat. The default is Client. For more, see [Game Server Stats](https://partner.steamgames.com/doc/features/achievements#game_server_stats).
* **Increment Only** \
  If set, this stat is only allowed to increase in value over time.
* **Max Change** \
  If set, sets a limit on the amount that the stat's value can change from one SetStat call to the next.
*   **Min Value**&#x20;

    If set, the minimum numerical value this stat may take. By default, the min is the minimum of the underlying numerical type (INT\_MIN or -FLT\_MAX).
*   **Max Value**&#x20;

    If set, the maximum numerical value this stat may take. By default, the max is the maximum of the underlying numerical type (INT\_MAX or FLT\_MAX).
*   **Default Value**&#x20;

    If set, the default value that this stat will initially be set to for a new user. If not set, the default value is zero.
*   **Aggregated**&#x20;

    If set, Steam will keep a global total for this stat. See Global Stats below for more information.
*   **Display Name**&#x20;

    The name of this stat when displayed in your app.

**AVGRATE** stats have the following additional properties:

* Window - The size of the "sliding window" used to average your data.

An **AVGRATE** stat is automatically averaged by Steam. See the [AVGRATE](https://partner.steamgames.com/doc/features/achievements#AVGRATE) section below for more information.\
\
Achievements have the following properties:

*   **ID**&#x20;

    An automatically-generated numerical ID for each achievement.
*   **API Name**&#x20;

    The string used to access this achievement using the API.
*   **Progress Stat**&#x20;

    It specifies a stat that's used as a progress bar in the community for this achievement. The achievement will also automatically unlock when the stat reaches the unlock value.
*   **Display Name**&#x20;

    The name of this achievement will be displayed in client notification pop-ups and the Community. May be localized.
*   **Description**&#x20;

    A description of this achievement, for displaying in the Community. May be localized.
*   **Set By**&#x20;

    Sets who can unlock the achievement. The default is client. For more, see [Game Server Stats](https://partner.steamgames.com/doc/features/achievements#game_server_stats).
*   **Hidden?**&#x20;

    If true, a "hidden" achievement does not show up on a user's Community page (at all) until they have achieved it.
*   **Achieved Icon**&#x20;

    The icon will be displayed when it is achieved.
*   **Unachieved Icon**&#x20;

    The icon to display when it is not yet achieved.

## AVGRATE stats

**AVGRATE** stats are designed to track averages over time—like “Points per Hour”—but with a key advantage: they respond to recent gameplay instead of being dragged down by older data.

#### Why Not Just Use Two Stats?

You _could_ track points per hour by creating two separate stats:

* `TotalPoints` (INT)
* `TotalPlayTimeHours` (FLOAT)\
  Then calculate: `TotalPoints / TotalPlayTimeHours`.

**The problem?**\
As the player logs more hours, that average becomes sluggish. If a player has 100 hours logged, any improvement in skill will barely move the average. It can take hours before players see any change, which isn’t useful for showing recent performance.

#### What AVGRATE Does Better

AVGRATE lets you define a _sliding time window_—say, the last 20 hours—so the average reflects recent gameplay, not a lifetime total.

#### Important Notes

* You can use any time unit (seconds, minutes, hours), just be consistent between the `Window` and `dSessionLength`.
* Use AVGRATE when you want averages that reflect current player performance, not lifetime summaries.

## Examples

### Set (Int & Float stats)

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

## C\#

```csharp
// Identify which stat
StatData statData = "API_NameHere"; // Use the API name you created in the Steamworks Developer Portal

// Set has an int and a float overload
statData.Set(42);
// or
statData.Set(42.0f);
```

For Steam Game Servers

```csharp
// Servers that have authenticated a user can request
// that user's stats, and when they have those stats, they can update them
CSteamID userId = new(); // This is just a stand-in for the ID of the user you want to read for
StatsAndAchievements.Server.RequestUserStats(userId, HandleStatsReceived);

StatsAndAchievements.Server.SetUserStat(userId, "API_NameHere", 42);
// or
StatsAndAchievements.Server.SetUserStat(userId, "API_NameHere", 42.0f);
```

The handler for the request user stats would look like this

```csharp
private void HandleStatsReceived(GSStatsReceived_t results, bool arg2)
{
    // results.m_eResult: The EResult of the request
    // results.m_steamIDUser: Which user you got the results for
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Update (AVGRATE stats)

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

## C\#

```csharp
// Identify which stat
StatData statData = "API_NameHere"; // Use the API name you created in the Steamworks Developer Portal

// The Set overload that takes a value and a length is how you update average stats
float value = 42f;
double length = 14;
statData.Set(value, length);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Read Stat

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

## C\#

```csharp
// Identify which stat
StatData statData = "API_NameHere"; // Use the API name you created in the Steamworks Developer Portal

// Get the value as a float
float FloatValue = statData.FloatValue();

// Get the value as an int
int IntValue = statData.IntValue();
```

For Steam Game Servers

```csharp
// Steam Game Servers can read stats for users
CSteamID userId = new(); // This is just a stand-in for the ID of the user you want to read for

// First, the server must request the user's stats, which can only be done after authentication
StatsAndAchievements.Server.RequestUserStats(userId, HandleStatsReceived);

// When the HandleStatsReceived has completed, you can then read the stat values 
// Get the value as a float
StatsAndAchievements.Server.GetUserStat(userId, "API_NameHere", out float floatValue);

// Get the value as an int
StatsAndAchievements.Server.GetUserStat(userId, "API_NameHere", out int intValue);
```

The HandleStatsReceived noted above would look like this

```csharp
private void HandleStatsReceived(GSStatsReceived_t results, bool arg2)
{
    // results.m_eResult: The EResult of the request
    // results.m_steamIDUser: Which user you got the results for
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

