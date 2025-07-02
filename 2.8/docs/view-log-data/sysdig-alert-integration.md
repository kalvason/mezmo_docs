---
type: page
title: Sysdig Alert Integration
listed: true
slug: sysdig-alert-integration
description: 
index_title: Sysdig Alert Integration
hidden: 
keywords: 
tags: 
---


## About Sysdig Alert Integration

Mezmo integrates with Sysdig and allows you to configure alerts, based on log lines ingested by Mezmo, that trigger new events in your Sysdig instance. This integration provides access to custom log metrics data that is useful in debugging and monitoring the health of a system.

For example, you can monitor deployments with a Mezmo view that queries for specific errors during deployment. Then attach to the view an integrated alert  that is configured to trigger when more than the expected number of logs with that specific error appear. The integrated alert then sends that event to the Sysdig Events feed.

### Considerations

- Alerts are supported only for Sysdig Monitor events.
- Only presence alerts, not absence alerts, are supported.
- The Sysdig event timestamp will reflect when the alert is received by Sysdig. This will be displayed in the timezone as configured in the Sysdig UI (either local, or UTC)
- The event "description" field will contain a formatted version of the first log line that triggered the alert. Note that the timestamp of this line will differ from the Sysdig event timestamp depending on the configuration of the Mezmo alert.

## Integrating with Sysdig

1. In either the View-specific or preset Alert modal, select the Sysdig logo to configure a Sysdig alert channel.

{% image url="https://uploads.developerhub.io/prod/2KW7/k9j9xzzuqai3cz7pr3ybj2mbkgm6nm1tbr2o2k9w7s3b9w0xion2yi3wvx3x7m5r.png" mode="responsive" height="982" width="839" %}
{% /image %}

2. On the Alert modal, define the alert properties.
3. Enter the Sysdig **API key**. You can find this value by clicking on your user icon in the lower left corner of the Sysdig Monitor UI, and then selecting  **Settings** to display your User Profile page with the "Sysdig Monitor API Token."
4. Enter the **Sysdig instance URL**. This URL is the base URL for your Sysdig Monitor instance. You can choose from the dropdown list of available URLs, or enter your own (for on-premise or other Sysdig installations)
5. Select the **Severity** level for the alert, as you want it to appear in the Sysdig application UI. For example, if the query upon which your view is based searches for multiple failed log-in attempts, you could select **High** as the severity label.

{% callout type="info" title="Note" %}
By default, the **Severity** level is set to `info`.
{% /callout %}

6. Click **Save Alert**.

When the parameters of the alert's conditions are met, the Sysdig UI displays the alerts in the Events feed.