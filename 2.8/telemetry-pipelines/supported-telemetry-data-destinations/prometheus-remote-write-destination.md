---
type: page
title: Prometheus Remote Write
listed: true
slug: prometheus-remote-write-destination
description: 
index_title: Prometheus Remote Write
hidden: 
keywords: 
tags: 
---

## Description

You can send your metrics to any destination that accepts data using the Prometheus Remote Write protocol (such as sending metrics to Grafana).

## Configuration

You can configure the destination using these options.

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| End-to-end acknowledgement | Enable this option to receive verification that log data is being received by Prometheus. | 
| Strategy | The authentication strategy to use. | 
| Endpoint | The endpoint for the Prometheus instance where you want to send your logs. | 
{% /table %}