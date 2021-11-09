# Set User Avatar

## Introduction

A simple componenet meant to be attached to a UnityEngine.UI.RawImage

This can update the raw image with the indicated user's avatar and can optionally pull the local user's data on start up.

## Definition

### Fields and Attributes

| Type     | Name         | Comments                               |
| -------- | ------------ | -------------------------------------- |
| RawImage | image        | The image to assigne the avatar to     |
| bool     | useLocaluser | should we load the local user on start |



### Events

#### Loaded

Occurs when the texture is loaded

### Methods

```csharp
public void LoadAvatar(user);
```

Load the selected user's avatar image.
