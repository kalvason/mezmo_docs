---
type: page
title: Checkly
listed: true
slug: checkly
description: 
index_title: Checkly
hidden: 
keywords: 
tags: 
---


## Description

[Checkly](https://www.checklyhq.com/) enables you to quickly test, monitor, and observe your apps and APIs using Playwright and OpenTelemetry in a single workflow.

## Configuration

Checkly is an OTLP-compliant sender, so you can use the [auto$](/telemetry-pipelines/open-telemetry-traces-source) Source to ingest Checkly data into your Pipeline.

### Configuration Options

{% table widths="" %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| `URL/Endpoint` | The unique URL for your Checkly instance | 
| `Token` | Token used for authorization to Checkly | 
{% /table %}

{% /table %}