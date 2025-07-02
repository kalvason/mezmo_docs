---
type: page
title: Generate Service and Ingestion Keys
listed: true
slug: ingestion-key
description: Your Mezmo account includes private service and ingestion keys you can use for sending log data and interacting with the API
index_title: Generate Service and Ingestion Keys
hidden: 
keywords: 
tags: 
---

You use the personalized, private service and ingestion keys associated with your account to connect Mezmo to third-party applications and services. They enable programs such as log collectors to authenticate with Mezmo without requiring you to share your account details, and let you manage your log data with the Mezmo REST API.

{% callout type="error" title="Keep Your Keys Secret" %}
Anyone who has access to your service and ingestion keys can send or retrieve logs to or from your account with no additional authentication. Be sure to keep your API keys secret.
{% /callout %}

## Ingestion and Service Keys

There are two types of keys you can manage, **Ingestion Keys** and **Service Keys**.

### Ingestion Keys

Ingestion keys are used by log collectors like the Mezmo Agent to send log data to Mezmo, and are also used in commands for the Ingest API. You can have up to 10 ingestion keys active at a time.

### Service Keys

Service keys are used to retrieve logs via the Mezmo API endpoints for Export, and to manage Mezmo Views, Alerts, and other configuration objects using the Configuration endpoints. You can have up to 20 service keys active at a time.

## Access and Generate New Keys

1. Log in to [the Mezmo Web App](https://app.logdna.com/account/signin).
2. Go to **Settings &gt;** **Organization &gt; API Keys**.
3. To generate additional ingestion keys, click **Generate Ingestion Key** for up to a total of 10 keys.
4. To generate additional service keys, click **Generate Service Key** for up to a total of 20 keys.
5. Remove an ingestion key by clicking the X next to it.
Note that any applications actively using this key will no longer be able to send logs to your account

{% image url="https://uploads.developerhub.io/prod/2KW7/j42gmtllmavb26q8m4e1r3drgyd9dfa4zhr2r7ln5m4yy8qwo1iksokj1fupb75c.png" caption="Access to the API Keys through **Settings &gt; Organization**" mode="responsive" height="382" width="220" %}
{% /image %}