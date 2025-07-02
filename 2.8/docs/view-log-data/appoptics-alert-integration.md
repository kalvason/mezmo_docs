---
type: page
title: AppOptics Alert Integration
listed: true
slug: appoptics-alert-integration
description: 
index_title: AppOptics Alert Integration
hidden: 
keywords: 
tags: 
---


Mezmo’s alert integration with AppOptics interfaces with the [App Optics Measurement API](https://docs.appoptics.com/api/#measurements) and allows alerts set in Mezmo to create measurements in AppOptics.

## Integrating with AppOptics

On the alerts creation page, select the AppOptics logo.

To find an API token, in your AppOptics dashboard, go to [Settings → API Tokens ](https://my.appoptics.com/organization/tokens)page to copy an existing or create a new API token with “Record Only” permission.

{% image url="https://uploads.developerhub.io/prod/2KW7/h3u2sns7lk9rnw5x9eiwzn4wy58s8uxqkeem3kgp6xoidjjln8nr7bssm5y4gl7s.png" mode="responsive" height="387" width="717" %}
{% /image %}

Remember to save your alert so that your  alerts will now trigger in AppOptics and new alerts will be in yourAppOptics dashboard. Specifically, new alerts can be found by navigating to: AppOptics -&gt; Dashboards and Metrics -&gt; mezmo.alerts.

{% image url="https://uploads.developerhub.io/prod/2KW7/h3u2sns7lk9rnw5x9eiwzn4wy58s8uxqkeem3kgp6xoidjjln8nr7bssm5y4gl7s.png" mode="responsive" height="387" width="717" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/q1n5ulylkflwb8f86z1z7i9n77enfdgbgibp7szb1b3pxmjnw3qnpglfmanrb8j8.png" mode="responsive" height="1014" width="1600" %}
{% /image %}

## Testing your AppOptics alert integration

Before saving your AppOptics alert, you can also trigger a test alert with test data. As long as you have pasted a valid API token from AppOptics, you will be able to create a test alert.