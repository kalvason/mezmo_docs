---
type: page
title: Checkly
listed: true
slug: checkly-destination
description: 
index_title: Checkly
hidden: 
keywords: 
tags: 
---


## Description

[Checkly](https://www.checklyhq.com/) enables you to quickly test, monitor, and observe your apps and APIs using Playwright and OpenTelemetry in a single workflow.

## Configuration

You can send data to a Checkly using the [auto$](/telemetry-pipelines/opentelemetry-destination) Destination.

### Configuration Options

{% callout type="info" title="Checkly Access Key" %}
You will also need to provide the access key for your Checkly instance.
{% /callout %}

{% table widths="" %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Collector Endpoint | [`https://otel.eu-west-1.checklyhq.com/`](https://otel.eu-west-1.checklyhq.com/) | 
{% /table %}

{% /table %}

### Route Processor Configuration

Because Checkly only accepts Checkly-related spans, you will need to configure a [auto$](/telemetry-pipelines/route-processor) to send those spans to your destination.  Use this conditional statement to route the spans to the destintation.

{% code %}
{% tab language="bash" %}
if trace_state: checkly=true
{% /tab %}
{% /code %}