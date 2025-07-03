---
type: page
title: Loki
listed: true
slug: loki-destination
description: 
index_title: Loki
hidden: 
keywords: 
tags: 
---

## Description

You can send your logs to any Loki destination (like Grafana Logs).

## Configuration

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| End-to-end Acknowledgement | Enable this option to receive verification that log data is being received by Loki.. | 
| Strategy | The authentication strategy to use for the endpoint. | 
| Codec | The coded to use in encoding events. | 
| Endpoint | The base URL for your Loki instance. | 
| Path | The path to use to your Loki instance. The default is `/loki/api/v1/push`. | 
| Loki Labels | The key:value pairs to use in identifying the data you are sending to Loki. | 
{% /table %}