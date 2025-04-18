---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Currency

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public static class Currency
```

A simple class used to list the supported currency codes available in Steam and to fetch the string symbols of those codes.

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
