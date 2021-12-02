# NFT Balance Result

## Introduction

Returned by Wallet API calls and defines the NFT contents found

```csharp
public class NFTBalanceResult : BGSDKBaseResult
```

### Fields and Attributes

| Type         | Name   | Notes                          |
| ------------ | ------ | ------------------------------ |
| List\<Token> | result | The collection of tokens found |

The result list contains a list of NFTBalanceResult.Token objects as is typical with blockchain most of this data is meaningless to a game however the important aspect is the TokenTypeId or better still the TokenType its self.

The typical use case is that you need to match a token owned by a user to some game object such as the Token types defined in your BGSDK Settings. The system does this for you when you call TokenType e.g.

```csharp
var myTokenType = result[0].TokenType;
```

When you call Token Type the system will inspect the data stored in the result to determin the token type ID, it will then check your current BGSDK Settings object and find the token definition that has a matching type ID if any. If none is found it will return null.
