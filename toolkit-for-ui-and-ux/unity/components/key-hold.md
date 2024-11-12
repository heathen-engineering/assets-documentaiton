# Key Hold

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

Ever play a game that asked you to push an hold a button for some period of time to activate the action?

The Key Hold event components do just that and are designed to work with Unity's "legacy Input System"

This component is available in two flavors

### KeyHoldGameEvent

For use with Heathen Game Events

### KeyHoldUnityEvent

For use with standard Unity Events

## Definition

### Fields and Attributes

<table><thead><tr><th width="184.37677897593124">Type</th><th width="194.9100036101649">Name</th><th width="333.5407480296978">Notes</th></tr></thead><tbody><tr><td>KeyCode[]</td><td>keys</td><td>The keys to monitor, all keys must be held</td></tr><tr><td>float</td><td>holdTime</td><td>How long the action should be held</td></tr><tr><td>bool</td><td>useUnscaledTime</td><td>Should time scale be considered</td></tr></tbody></table>

### Events

#### Start

Occurs when the action is first started to be held

#### Cancel

Occurs when the action is released before a complete

#### Complete

Occurs when the action is fully held for its duration

#### Progressed

Updated per frame noting the total progress
