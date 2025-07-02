---
type: page
title: Mezmo Log Analysis
listed: true
slug: mezmo-log-analysis-pipeline-destination
description: 
index_title: Mezmo Log Analysis
hidden: 
keywords: 
tags: 
---

## Description

Sending your pipeline data to Mezmo Log Analysis enables you to use features like [JSON Field Search](/docs/search-json-fields), and [Views and Alerts](/docs/view-log-data), to analyze and visualize your log data. 

## Configuration

You can send data to any Log Analysis account, not just the current account. If you want to use your current account, use the Ingestion Key associated with it as described in the **Configuration Options**. 

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Mezmo Host | The URI for your Mezmo Log Analysis host environment. This option is auto-configured based on your Mezmo account. | 
| Hostname | The tag to use to identify the origin of your logs. | 
| Ingestion Key | Your Mezmo ingestion key. You can find this by logging into the Mezmo Web App and navigating to **Settings &gt; Organization &gt; API Key**. | 
{% /table %}