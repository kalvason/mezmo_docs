---
type: page
title: Mezmo Agent/Mezmo OTel Exporter
listed: true
slug: mezmo-agent-pipeline-source
description: 
index_title: Mezmo Agent/Mezmo OTel Exporter
hidden: 
keywords: 
tags: 
---

## Description

The Mezmo Agent Pipeline Source enables streaming of log data from the Mezmo Agent directly to your Pipeline.

## Mezmo Agent Configuration

You must configure your Agent to point to the pipeline data ingestion endpoint in order to use this source:

 `pipeline.app.mezmo.com`. 

This is not the same as the existing Mezmo ingestion API endpoint.

To use the Mezmo Agent as a source for Mezmo Pipelines, you must add your API 
key into the configuration of the Agent. You can find this by logging into the Mezmo Web App and navigating to **Settings &gt; Organization &gt; API Keys**. 

You can find more information about configuring the Mezmo Agent in the topic [auto$](/docs/introducing-the-agent).

## Mezmo OTel Exporter Configuration

{% synced id="otel-exporter" %}
{% /synced %}