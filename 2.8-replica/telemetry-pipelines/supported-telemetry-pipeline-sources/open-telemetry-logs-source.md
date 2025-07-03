---
type: page
title: OpenTelemetry Logs
listed: true
slug: open-telemetry-logs-source
description: 
index_title: OpenTelemetry Logs
hidden: 
keywords: 
tags: 
---


## Description

You can send your logs to a Mezmo Pipeline via any OTLP compliant sender.

{% callout type="info" title="OTLP Format" %}
Mezmo currently requires that you use the HTTP transport for your payload, not the standard gRPC transport mechanism, to send in data via OTLP
{% /callout %}

## Configuration

The OTLP Logs source provides a unique endpoint URL that uses **Bearer Token** authentication. You can obtain the unique endpoint and Bearer Token from the Mezmo pipeline app when you create a new OTLP Logs source.

### Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| url / endpoint | unique URL for your OTLP source | 
| token | token used for authorization for your OTLP source | 
{% /table %}

{% /table %}

### OpenTelemetry Collector Configuration

To configure an OTel collector to export to Mezmo, you can add the following to your exporters section of your OTel Collector config file:

{% code %}
{% tab language="yaml" %}
exporters:
otlphttp//mezmo-logs:
endpoint: "https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;"
headers:
Authorization: "&lt;YOUR_PIPELINE_INGEST_KEY&gt;"
{% /tab %}
{% /code %}

{% callout type="warning" title="Must Match the OpenTelemetry Logs URL" %}
The endpoint in the exporters configuration must exactly match the URL provided by the OpenTelemetry Logs. You don't need to specify the `/v1/logs` path, which will otherwise by ignored by the Source.
{% /callout %}