---
type: page
title: Datadog Metrics
listed: true
slug: datadog-metrics-destination
description: 
index_title: Datadog Metrics
hidden: 
keywords: 
tags: 
---

## Description

This destination allows you to send metrics data to Datadog.

## Configuration

You can only use the Datadog Metrics destination with the [Datadog Agent](https://docs.mezmo.com/telemetry-pipelines/mezmo-datadog-source-source), [HTTP Source ](/telemetry-pipelines/http-source)and the [Prometheus Remote Write Source](/telemetry-pipelines/prometheus-remote-write-destination) as the sources configured in your pipeline.

Metrics sent from Mezmo to Datadog are considered **Custom Metrics** within Datadog and will have an impact on your bill. 

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Datadog API Key | The API key for your Datadog application. | 
| Compression | Options for compressing your metrics. | 
| Datadog Site | The Datadog region to send your metrics to. | 
{% /table %}