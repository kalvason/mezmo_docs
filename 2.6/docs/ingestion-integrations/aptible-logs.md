---
type: page
title: Aptible
listed: true
slug: aptible-logs
description: Mezmo provides an integration to stream logs from Aptible, and options to enter hostnames, tags, and apps to distinguish your Aptible logs from logs from other sources.
index_title: Aptible
hidden: 
keywords: 
tags: 
---

## Set Up Aptible Log Ingestion

Follow the instructions in the Mezmo Web App to set up Aptilbe log ingestion using your Mezmo ingestion key.

1. Log in to [the Mezmo Web App](https://app.Mezmo.com/account/signin).
2. In the bottom section of the left-hand navigation, click the **Add Log Sources** icon.
3. Under **Via platform**, click **Aptible**.
4. Follow the instructions to set up Aptible log ingestion.
Note that your ingestion key is automatically inserted into the configuration code.

{% callout type="warning" title="Multi-Line Parsing Not Supported" %}
Because of the way Aptible interacts with the Mezmo Ingestion API, our integration does not support multi line parsing. This means that stack traces may be split up into several log lines, instead of being represented as a single entity.
{% /callout %}