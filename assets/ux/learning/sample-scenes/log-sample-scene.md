# Log Sample Scene

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../core-concepts/">User eXperience Tools</a></td><td><a href="../ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../../.gitbook/assets/image (180) (1) (1) (1).png>)

This scene demonstrates the use of Heathens extended system log. Our log system works with Unity's built in log to gather data via simple Debug.Log calls but does so in greater details, gathers additional system informaiton and can package its log as a more human friendly simple text log, as a feedback tool friendly JSON object or as byte\[] for easy transmission over a network.

The Heathen log is designed to empower your operations team to gather more meainingful feedback from users and make more informed decisions with support and maintenance. Our tools are easy to connect with any feedback, support or reporting tool you may already be using and includes helpers to get you started if you haven't yet implamented a feedback system.

## What do I learn?

1. Outputting the log as text or json ... byte\[] is also available but not useful to prenset in Unity's UI :smile:
2. How to access the Knowledge Base (where you are now)
3. How to access the support [Discord ](https://discord.gg/6X3xrRc)
4. How to leave a review 😉

## Objects

### Managers

This game object implaments a simple sample script LogExampleScrtipt. This script simply enables the log on start up and is called by the UI buttons to output the logs text and json to a UI element.
