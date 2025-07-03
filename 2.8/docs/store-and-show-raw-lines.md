---
type: page
title: Enable Raw Line Storage
listed: true
slug: store-and-show-raw-lines
description: 
index_title: Enable Raw Line Storage
hidden: 
keywords: 
tags: 
---

Mezmo [automatically parses log lines](/docs/log-parsing) received from [various sources](/docs/ingestion-integrations) to surface the content of log lines, so your account isn’t charged for retaining the entirety of bulky log line formats. However, there may be situations where you want to receive the raw line in its entirety, including the original format. In those situations, you can enable saving and viewing raw lines for your account.

{% callout type="info" title="Owners and Admins Only" %}
The option to store and show raw log lines is only available to Owners and Admins of the organization. The toggle to turn this selection on and off will not be visible to other roles.
{% /callout %}

{% callout type="warning" title="Storage Costs May Increase" %}
Enabling this feature may result in the retention of more data in your account, and your storage costs may increase accordingly. Most accounts will only see a minor increase in storage costs, but certain log formats will increase costs more than others. Github and Akamai as log sources tend to be more verbose in the raw form, and are anticipated to lead to greater cost increases. Other log sources that have large raw payloads may also result in increased costs.
{% /callout %}

1. In the left-hand navigation in the [Web App](https://app.mezmo.com), go to **Settings &gt; Organizations &gt; General**.
2. Under **Store and Show Raw Line**, move the toggle switch to **On**.

Within five minutes of toggling this feature on, your raw log lines will be sent to storage.