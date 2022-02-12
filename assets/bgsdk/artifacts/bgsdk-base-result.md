# BGSDK Base Result

## Introduction

Most callbacks have some form of result message they respond with, the BGSDK Base Result is the base class for all of the BGSDK's result responses.

```csharp
public class BGSDKBaseResult
```

### Fields and Attributes

| Type      | Name      | Notes                                                                                                |
| --------- | --------- | ---------------------------------------------------------------------------------------------------- |
| bool      | success   | If true then the call result is a success                                                            |
| bool      | hasError  | If true then an error message and code should be present                                             |
| string    | message   | Typically stores error messages                                                                      |
| long      | httpCode  | The HTTP code such as 500 ... this indicates the standard response code returned by the Web API call |
| Exception | exception | If a system exception was thrown it will be stored here                                              |
