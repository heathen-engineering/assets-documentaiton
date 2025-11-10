---
description: public struct AppData
---

# AppData

Represents the ID of a Steam App and exposes the core tools and features of the Steam API about Steam Apps.

## Fields and Attributes

### App ID

```csharp
public Steamworks.AppId_t AppId { get; }
```

The native Steamworks.AppId\_t id of the app

***

### ID

```csharp
public uint Id { get; }
```

Returns the primitive System.UInt32 value of the id

***

### Is Me

```csharp
public bool IsMe { get; }
```

Returns true if this AppData represents the current App being ran

***

### Me

```csharp
public static AppData Me { get; }
```

Return the AppData object representing this program's App

***

### Name

```csharp
public string Name { get; }
```

Gets the name if loaded, returns Unknown until names have been loaded

> you can call AppData.LoadNames(Action) to load the names for all apps. you can call AppData.GetName(System.Action{String,Boolean}) to load the names if needed and then return this apps name when loaded

***

### Names Loaded

```csharp
public static bool NamesLoaded { get; }
```

True if the system has loaded the set of App names from Steam's web API

***

## Functions

### Compare To

```csharp
public int CompareTo(AppData other);
// or
public int CompareTo(AppId_t other);
// or
public int CompareTo(uint other);
// or
public int CompareTo(ulong other);
```

ICompare for AppData, AppId\_t, uint and ulong comparisons

***

### Equals

```csharp
public bool Equals(AppData other);
// or
public override bool Equals(object obj);
// or
public bool Equals(AppId_t other);
// or
public bool Equals(CGameID other);
// or
public bool Equals(uint other);
// or
public bool Equals(ulong other);
```

Check for equality&#x20;

***

### Get

```csharp
public static AppData Get();
// or
public static AppData Get(DlcData dlcData);
// or
public static AppData Get(AppId_t appId);
// or
public static AppData Get(CGameID gameId);
// or
public static AppData Get(uint appId);
// or
public static AppData Get(ulong gameId);
```

Get an app data based on various inputs, the empty parameter option will return the AppData for the currently initialised App.

***

### Get Hash Code

```csharp
public override int GetHashCode()
```

Return a Has Code for the object.

***

### Get Name

```csharp
public bool GetName(out string name)
// or
public void GetName(Action<string, bool> callback)
```

Gets the name of the app if available. If you provide a callback, we will request the list of names if not present and return the result from that.

***

### Load Names

```csharp
public static void LoadNames(Action callback)
```

Request the list of app names and notify when complete.

***

### Open My Steam Store

```csharp
public static void OpenMySteamStore([EOverlayToStoreFlag flag = 0])
```

Open the Steam store to this app's store page with the indicated flags.

***

### Open Steam Store

```csharp
public static void OpenSteamStore(AppData app, [EOverlayToStoreFlag flag = 0]);
// or
public void OpenSteamStore([Steamworks.EOverlayToStoreFlag flag = 0]);
```

Open the Steam store to the indicated app

***

### To String

```csharp
public override string ToString();
```

String value of the ID

***

## Operators

### Assignment

```csharp
```



***

### Equality

```csharp
```



***
