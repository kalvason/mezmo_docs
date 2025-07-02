---
type: page
title: PagerDuty Alert Integration
listed: true
slug: pagerduty-alert-integration
description: 
index_title: PagerDuty Alert Integration
hidden: 
keywords: 
tags: 
---



## About PagerDuty Alert Integration

Mezmo’s alert integration with PagerDuty interfaces with  [PagerDuty Event API](https://developer.pagerduty.com/docs/events-api-v2/overview/) and allows alerts sent from Mezmo to trigger events in PagerDuty.

For general information on alerts and instructions on how to create alerts, follow the documentation instructions listed in the [“How to create an alert”](/docs/alerts#how-to-create-an-alert) section of the documentation.

## Integrating with PagerDuty

On the alerts creation page, select the PagerDuty logo. Define the alert properties ([learn more here](/docs/alerts#types-of-alerts)) and click the **Add PagerDuty** button to connect your PagerDuty account.



{% image url="https://uploads.developerhub.io/prod/2KW7/fscusmyp87hri934qjtuu3tj62d1uvlnbdw9czuk2l6of5fr2icet5n5s0snkbjk.png" caption="" mode="responsive" height="524" width="716" %}
{% /image %}



You will be directed to PagerDuty to authorize the integration, using your email address and password for your PagerDuty account.



{% image url="https://uploads.developerhub.io/prod/2KW7/fscusmyp87hri934qjtuu3tj62d1uvlnbdw9czuk2l6of5fr2icet5n5s0snkbjk.png" caption="" mode="responsive" height="524" width="716" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/5vwrmljpi1d1ycrohbnfozt48vtdhzqx9uzyawckj2p0oum425deh55x3xeogb4o.png" caption="" mode="responsive" height="1644" width="898" %}
{% /image %}



After authorization, you are prompted to select the PagerDuty service **logging alerts** and then click **Connect**.



{% image url="https://uploads.developerhub.io/prod/2KW7/fscusmyp87hri934qjtuu3tj62d1uvlnbdw9czuk2l6of5fr2icet5n5s0snkbjk.png" caption="" mode="responsive" height="524" width="716" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/5vwrmljpi1d1ycrohbnfozt48vtdhzqx9uzyawckj2p0oum425deh55x3xeogb4o.png" caption="" mode="responsive" height="1644" width="898" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/3il6eg0mlyolu0k8fgo6fsyqmtffncfptzigntp5zzxayili97o1urrx1n8tpjhg.png" caption="" mode="responsive" height="972" width="1250" %}
{% /image %}



After completing the connection, remember to save your Mezmo alert so that your alerts will trigger in PagerDuty and new alerts display in your PagerDuty incidents dashboard.



{% image url="https://uploads.developerhub.io/prod/2KW7/fscusmyp87hri934qjtuu3tj62d1uvlnbdw9czuk2l6of5fr2icet5n5s0snkbjk.png" caption="" mode="responsive" height="524" width="716" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/5vwrmljpi1d1ycrohbnfozt48vtdhzqx9uzyawckj2p0oum425deh55x3xeogb4o.png" caption="" mode="responsive" height="1644" width="898" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/3il6eg0mlyolu0k8fgo6fsyqmtffncfptzigntp5zzxayili97o1urrx1n8tpjhg.png" caption="" mode="responsive" height="972" width="1250" %}
{% /image %}





{% image url="https://uploads.developerhub.io/prod/2KW7/tdet6zfj15ko69694zrhlyd87vuxp0igimabjjtjjmr611hk520ffhj4r3naaoh7.jpg" caption="" mode="responsive" height="1272" width="2132" %}
{% /image %}



## Testing Your PagerDuty Integration

You can choose trigger a test alert with test data, even before saving your PagerDuty alert. As long as you have selected a connected source from PagerDuty, you will be able to create a test alert.

## Deleting Your PagerDuty Integration

1. Log in to the Mezmo Web App.
2. Go to **Settings &gt; Integrations**.
3. Select your PagerDuty integration to open its **Settings** page.
4. Click the **X** next to the Service you want to delete.
5. Click *_Yes, delete *_in the confirmation dialog to remove the service.

## Limitations on PagerDuty data payload

Because of [PagerDuty integration limitations](https://developer.pagerduty.com/docs/events-api-v2/overview/), we trim all requests to be at most 400 kilobytes.



