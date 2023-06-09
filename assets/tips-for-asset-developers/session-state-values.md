---
description: Surviving recompile and reload
---

# Session State Values

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../steam/steam.md">steam.md</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

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
