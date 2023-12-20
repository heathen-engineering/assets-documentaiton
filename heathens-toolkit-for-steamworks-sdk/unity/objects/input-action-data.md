---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Input Action Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct InputActionData;
```

## Fields and Attributes

<table><thead><tr><th width="181.56643368118847">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>InputHandle_t</td><td>controller</td><td>The controller this action data was read from</td></tr><tr><td>InputActionType</td><td>type</td><td>Analog or Digital </td></tr><tr><td>bool</td><td>active</td><td>Is this action active e.g. part of an active set or layer</td></tr><tr><td>EInputSourceMode</td><td>mode</td><td>Only used for analog actions, indicates the type of analog action simulated e.g. mouse, stick, etc..</td></tr><tr><td>bool</td><td>state</td><td>True if this action is active. For analog actions this is true if either x or y is non-zero</td></tr><tr><td>float</td><td>x</td><td>For analog actions this indicates the x axis</td></tr><tr><td>float </td><td>y</td><td>For analog actions this indicates the y axis</td></tr></tbody></table>

