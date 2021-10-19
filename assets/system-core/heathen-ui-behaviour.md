---
description: A better more friendly MonoBehaviour experience ... Now with RectTransform
---

# Heathen UI Behaviour

## Introduction

This can be used in place of MonoBehaviour and adds support for Scriptable Tags and Heathen's SelfTransform which offers a more performant approch to get a componenets root transform than the standard unity `GameObject.transform as RectTransform` option.

## Members

### Tags

```csharp
public List<ScriptableObject> tags;
```

### Self Transform

```csharp
private RectTransform _selfTransfrom;
public RectTransform SelfTransfrom
{
    get
    {
        if(_selfTransform == null)
            _selfTransfrom = GetComponenet<RectTransfrom>();
        
        return _selfTrasnform;
    }
}
```
