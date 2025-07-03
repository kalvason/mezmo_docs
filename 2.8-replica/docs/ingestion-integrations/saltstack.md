---
type: page
title: SaltStack
listed: true
slug: saltstack
description: Mezmo provides an integration to stream, aggregate, and gain insights from SaltStack logs
index_title: SaltStack
hidden: 
keywords: 
tags: 
---


The Mezmo Salt deployment integration listens for your Salt state events and sends the event information to Mezmo.

## Set Up SaltStack Log Ingestion

Follow the instructions in the Mezmo Web App to set up SaltStack log ingestion using your Mezmo ingestion key.

1. Log in to [the Mezmo Web App](https://app.mezmo.com/account/signin).
2. In the bottom section of the left-hand navigation, click **Help**.
3. Select **Add Log Sources**.
4. Under **Via platform**, click **SaltStack**.
5. Follow the instructions to set up SaltStack log ingestion.
Note that your Mezmo ingestion key is automatically inserted into the configuration code.

{% callout type="info" title="Viewing Salt States" %}
If you select the **Salt** app inside the [All Apps filter menu](https://docs.mezmo.com/docs/filters)), you can see the states applied across all your hosts. Filtering by a specific source will only show Salt states applied to that particular host.
{% /callout %}

{% image url="https://uploads.developerhub.io/prod/2KW7/gy90v5y1tnz67o2hqtbkmrthruo0aeuppkdmbzb26e7j81s3vmmiq16i1uelus23.png" mode="responsive" height="72" width="779" %}
{% /image %}