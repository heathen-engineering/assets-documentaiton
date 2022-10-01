# App.Web

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

### Namespace

```csharp
using AppWeb = HeathenEngineering.SteamworksIntegration.API.App.Web;
```

### Definition

```csharp
public static class App.Web
```

This leverages the ISteamApp interface from Valve's Steam Web API and exposes the features of that API in a C# and Unity centric way.

Note we do not attempt to expose authorized endpoints. That is much of the Steam Web API requires a publisher key and should be called from a trusted web server not from a game client or a game server. We only expose those web API calls that do not require a publisher key.

### What can it do?

The App Web interface can be used to read the news items from an App as they appear in Steam's backend such as patch notes and announcements and can also be used to find the published name of an app based on its app ID.

### SteamAppNews

This is a data structure used only by this API to handle the results of the NewsForApp call

```csharp
public struct SteamAppNews
{
    public uint appid;
    public SteamNewsItem[] newsitems;
    public uint count;
}
```

appid is the uint value of the AppId this data is related to

count is the total number of entries available in total (it seems)

newsitems is an array of SteamNewsItem objects as discribed below

```csharp
public struct SteamNewsItem
{
    public ulong gid;
    public string title;
    public string url;
    public bool is_external_url;
    public string author;
    public string contents;
    public string feedlabel;
    public long date;
    public string feedname
    public uint feed_type;
    public uint appid;
    
    public DateTime Date => get;
}
```

This object is not documented by Valve but its fields are mostly self explanitory. We added the Date field which will simply parse the "date" returned by Valve to a System.DateTime to make it easier to work with.



## Fields and Attributes

### IsAppsListLoaded

Check if the list of apps has been loaded from Steam API.

```csharp
public static bool IsAppsListLoaded => get;
```

## Methods

### LoadAppNames

```csharp
public static void LoadAppNames(Action callback)
```

Simply loads or attempts to load the list of apps available on Steam. This is required if you need to convert an AppId to the published app name for example if you wanted to list what game a user was playing based on that user's GameInfo.

### GetAppName

```csharp
public static bool GetAppName(AppId_t appId, out string name)
```

This overload assumes you have already loaded the app names. It returns true if the app was found and false otherwise. The out string name will be the name found if any.

```csharp
public static void GetAppName(AppId_t appId, Action<string, bool> callback)
```

This overload will load the app names for you if they are missing as such it is potentially asynchronious. That is if the names are already loaded it will invoke the callback instantly with the results otherwise it will load the names and invoke the callback when ready.

The call back should look as such

```csharp
void HandleResult(string name, bool ioFailure)
{
    if(ioFailure)
        Debug.LogError("Unable to read the name");
    else
        Debug.Log("Found: " + name);
}
```

### GetNewsForApp

```csharp
public static void GetNewsForApp(AppId_t appId, 
                                uint count, 
                                string feeds, 
                                string tags, 
                                Action<SteamAppNews, bool> callback)
```

This end point is not well documented by Valve however it does work to return the news entries for a given app and can be useful if you wanted to show that news in your game.

The appId is the app id you wish to return news for.

The count is how many entries you would like to get back, if you pass 0 it will default to 20

The feeds is a comma delimeted list of feeds to be read for example "steam\_community\_announcements"

The tags paramiter is a comma delimeted list of tags to filter on

Finally the callback, this will return the results as SteamAppNews object as well as an indication of error if any.

```csharp
void HandleResults(SteamAppNews news, bool ioFailure)
{
    if(ioFailure)
        Debug.LogError("Failed to read the news");
    else
    {
        foreach(var item in news.newsitems)
        {
            Debug.Log(
            "Title: " + item.title + 
            "\nContents: " + item.contents
            );
        }
    }
}
```

Note that the item contents will be using Steam mark up i.e. \[b]This is bold\[/b] its up to you to parse that however you see fit.
