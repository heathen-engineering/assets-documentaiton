---
description: A better more friendly MonoBehaviour experience
---

# Heathen Behaviour

## Introduction

This can be used in place of MonoBehaviour and adds support for Scriptable Tags and Heathen's SelfTransform which offers a more performant approch to get a componenets root transform than the standard unity `GameObject.transform` option.

## Members

### Tags

```csharp
public List<ScriptableObject> tags;
```

### Self Transform

```csharp
private Transform _selfTransfrom;
public Transform SelfTransfrom
{
    get
    {
        if(_selfTransform == null)
            _selfTransfrom = GetComponenet<Transfrom>();
        
        return _selfTrasnform;
    }
}
```

