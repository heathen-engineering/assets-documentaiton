# Workshop Browser

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of the [UGC Query Manager](../components/ugc-query-manager.md) to browse for Workshop items in game.

![](<../../../../.gitbook/assets/image (182) (1) (1).png>)

### What do I learn?

1. Using steam's [Input](../../api/input.md) API to handle controller input
2. Using [Input](../../api/input.md) API to get button images and names
3. Using the [UGC Query Manager](../components/ugc-query-manager.md) to query and iterate over items
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

### Instructions

1. Make sure you have Steam Client started and logged into a valid Steam user
2. Run the simulation
3. Click the Search button
   1. Observe records populate in the window below
4. Click the Next and Back buttons to iterate over pages
   1. Observer the records update to match the page
5. Type a string into the input field ... choose something you saw in the records this is a search string and we want to see results
   1. Observer that the records returned are different and correspond to your search string

## Objects

### Manager

The manager GameObject implements the [Steamworks Behaviour](../components/steamworks-behaviour.md) and the [UGC Query Manager](../components/ugc-query-manager.md) which are used by the scene to initialize Steam API and perform query operations against the Steam Workshop.

### Info Panel

The info panel uses standard Unity uGUI controls to display information and take user input e.g. the Search button and the Next and Back button ...&#x20;

For Search this button calls a method in the DEMO SCRIPTS object's `Scene7Behaviour` which simply reads the string from the InputField and starts the query via the [UGC Query Manager](../components/ugc-query-manager.md).

The Next and Back buttons call SetNextPage and SetPreviousPage on the [UGC Query Manager](../components/ugc-query-manager.md) updating the query page.

### DEMO SCRIPTS

This Game Object implements the Scene7Behaviour which is used by the UI controls to execute the query. This script also handles the returned results and instantiates the resulting records to the UI.
