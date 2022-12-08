---
description: Surviving recompile and reload
---

# Session State Values

## Overview

You can store simple primitive variables in the editors session state. These do not get wiped on code recompile and reload but are removed when the editor session is closed.

{% embed url="https://docs.unity3d.com/ScriptReference/SessionState.html" %}

These are important to use when your installing, updating or removing packages via script since any of those actions will cause a domain reload so all of your internal state data will be wiped... except of course the Session State Values.

What we do is set bools to know what we are doing and what we have done, in this way we insure we don't spam the user with a dialog or request every time the scripts compile. for example

_**Pseudo Code**_

```csharp
if(!SystemCoreIsInstalled
    && !SessionState.GetBool("SystemCoreHasAskedToInstall", false))
{
    SessionState.SetBool("SystemCoreHasAskedToInstall", true);
    AskToInstallSystemCore();
}
```

In the above example we check to see if we need to install System Core, and if we do and we have not already asked the user if we can ... then and only then do we ask the user.

This insures we never ask the user more than once per session.





```csharp
private IEnumerator InstallSystemCore()
{
    if(!SessionState.GetBool("SystemCoreInstalling", false))
    {
        SessionState.SetBool("SystemCoreInstalling", true);
        //Do Work
        SessionState.SetBool("SystemCoreInstalling", false);
    }
}
```

In this example we check if we are already installing System Core … if we are we do nothing … if we are not we indicate that we are now installing it by setting the SystemCoreInstalling value to true, then do our work, then set it back to false. In this way if another process trys to call Install System Core even if that is after a domain reload we will still not step on our own toes.
