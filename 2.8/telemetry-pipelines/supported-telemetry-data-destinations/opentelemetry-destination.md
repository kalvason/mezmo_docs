---
type: page
title: OpenTelemetry
listed: true
slug: opentelemetry-destination
description: 
index_title: OpenTelemetry
hidden: 
keywords: 
tags: 
---


## Description

You can send your logs, metrics and traces to any destination that accepts data using the OpenTelemetry protocol, for example Grafana, TelemetryHub, or New Relic.

## Data Type Compatibility

This table shows data type compatibility across Sources and Destinations within OpenTelemetry context.

{% table widths="215,84,0" %}

{% table %}
| Source Data Type |  | Destination Data Type | Compatibility | 
| ---- | ---- | ---- | ---- | 
| OpenTelemetry **-** **Log** | ➔ | OpenTelemetry **-** **Log** | ✅ | 
| Any Source **- Log** | ➔ | OpenTelemetry **-** **Log** | ❌ | 
| Any Source **- Metric** | ➔ | OpenTelemetry **-** **Metric** | ✅ | 
| OpenTelemetry **- Trace** | ➔ | OpenTelemetry **-** **Trace** | ✅ | 
| Any Source **- Trace** | ➔ | OpenTelemetry **-** **Trace** | ❌ | 
{% /table %}

{% /table %}

## Configuration

You can configure the Destination using these options.

### Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Collector Endpoint | The OpenTelemetry Collector URL that receives the data. Only http protocol is supported. No paths `/v1/logs` `/v1/metrics` `/v1/traces` needed, they will be added automatically based on a data type detected by the Destination. | 
| End-to-end acknowledgement | Enable this option to receive verification that OpenTelemetry data is being received by OTLP collector. | 
| Strategy | The authentication strategy to use. | 
| HTTP Headers | Additional headers to be sent with a request. The most common case is to set a secret key to authorize a request.\n\n\n\n**Note**: Authorization header is prohibited in case if some strategy has been already set up. | 
| Compression | Compression option: `none` or `gzip` to reduce network traffic | 
{% /table %}

{% /table %}