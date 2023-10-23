---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# Unreal Steam ID tools

## Blueprints

All Steam IDs can be expressed as simple value types such as int64 for Steam ID. Heathen provides a number of Blueprint nodes that help translate the IDs into and out of various data types such as Hex strings.

See the [Steam ID Tools article](../../heathens-steamworks-complete/unreal/blueprint-nodes/functions/steam-id-tools.md) for more information.

## C++

Working in C++ means you are working with the native CSteamID object which has methods for getting the Account ID and other parts of the ID. For example, if you wanted to convert an ID to a human-friendly Hex value

```cpp
FString::Printf(TEXT("%X"), id.GetAccountID());
```

Assuming the id was a CSteamID this would get the unique part of that ID, the account id and print it to a hex-style string.&#x20;

You can do the inverse then assuming `Fstring hexFriendId`, then

```cpp
FString HexValue = hexFriendId.Replace(TEXT("0x"), TEXT(""), ESearchCase::CaseSensitive);
int Result = FCString::Strtoi(*HexValue, nullptr, 16);

// Handle overflow or conversion errors
if (Result == 0 && HexValue != TEXT("0"))
{
    UE_LOG(LogTemp, Warning, TEXT("Hexadecimal string conversion overflow or error."));
}

CSteamID steamId(Result, EUniverse::k_EUniversePublic, EAccountType::k_EAccountTypeIndividual);
```
