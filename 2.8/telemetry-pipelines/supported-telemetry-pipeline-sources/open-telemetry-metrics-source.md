---
type: page
title: OpenTelemetry Metrics
listed: true
slug: open-telemetry-metrics-source
description: 
index_title: OpenTelemetry Metrics
hidden: 
keywords: 
tags: 
---

## Description

You can send your metrics to a Mezmo Pipeline via any OTLP compliant sender.

{% callout type="info" title="Info" %}
Mezmo currently requires that you use the HTTP transport for your payload, not the standard gRPC transport mechanism, to send in data via OTLP
{% /callout %}

## Configuration

The OTLP Metrics source provides a unique endpoint URL that uses **Bearer Token** authentication. You can obtain the unique endpoint and Bearer Token from the Mezmo pipeline app when you create a new OTLP Metrics source. When you [add the source to your Pipeline](/telemetry-pipelines/set-up-pipeline-sources), click on it and select Edit config. In the configuration settings, you will see the URL for the endpoint, and an option to generate a token. 

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| `url / endpoint` | unique URL for your OTLP source | 
| `token` | token used for authorization for your OTLP source | 
{% /table %}

### OpenTelemetry Collector Configuration

To configure an OTel collector to export to Mezmo, you can add the following to your exporters section of your OTel Collector config file:

{% code %}
{% tab language="yaml" %}
exporters:
  otlphttp/mezmo-metrics:
    endpoint: "https://pipeline.mezmo.com/v1/<YOUR ROUTE ID>"
    headers:
      Authorization: "<YOUR_PIPELINE_INGEST_KEY>"
{% /tab %}
{% /code %}

{% callout type="warning" title="Must Match the OpenTelemetry Metrics URL" %}
The endpoint in the `exporters` configuration must exactly  match the URL provided by the OpenTelemetry Metrics. You don't need to specify the  `/v1/metrics` path, which will otherwise by ignored by the Source.
{% /callout %}