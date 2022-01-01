# Currency

## Definition

```csharp
public static class Currency
```

A simple class used to list the supported currency codes available in Steam and to fetch the string symbole of those codes.

```csharp
public enum Currency.Code
```

A simple enum which lists all of the supported currency codes available in Steam

## Methods

### GetSymbole

```csharp
public static string GetSymbole(Currency.Code code);
```

Returns the string symbole used by this currency e.g. £, $, € etc.
