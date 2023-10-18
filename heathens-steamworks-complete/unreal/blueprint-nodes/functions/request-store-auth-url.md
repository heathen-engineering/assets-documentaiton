---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🔵 Request Store Auth URL

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Requests a URL which authenticates an in-game browser for store check-out, and then redirects to the specified URL.

As long as the in-game browser accepts and handles session cookies, Steam microtransaction checkout pages will automatically recognize the user instead of presenting a login page.

{% hint style="info" %}
The URL has a very short lifetime to prevent history-snooping attacks, so you should only call this API when you are about to launch the browser, or else immediately navigate to the resulting URL using a hidden browser window.
{% endhint %}

{% hint style="info" %}
The resulting authorization cookie has an expiration time of one day, so it would be a good idea to request and visit a new auth URL every 12 hours.
{% endhint %}

### Return Value

**true** if the Steam client currently has a live connection to the Steam servers; otherwise, **false** if there is no active connection due to either a networking issue on the local machine, or the Steam server is down/busy.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (312).png" alt=""><figcaption></figcaption></figure>
