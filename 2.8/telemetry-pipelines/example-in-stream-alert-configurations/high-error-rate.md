---
type: page
title: High Error Rate
listed: true
slug: high-error-rate
description: 
index_title: High Error Rate
hidden: 
keywords: 
tags: 
---

This is an example of an alert that is triggered when a high rate of errors is detected. This example assumes there is a [auto$](/telemetry-pipelines/filter-processor) or [auto$](/telemetry-pipelines/route-processor) that allows only Metric events, specifically `HTTP Status-5xx` errors. Check out the [auto$](/practioner-guide-data-optimization/pipeline-module--route) topic for an example with `HTTP Status-200` messages. 

## General Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Name | High rate of 5xx errors | 
| Description | Detects high number of 5xx errors per application | 
{% /table %}

## Evaluation and Condition Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Alert Type | Threshold Alert | 
| Event Type | Metric | 
| Group by Field Paths | `.app` | 
| Operation | Sum | 
| Window Type | Tumbling | 
| Window Duration (minutes) | 15 | 
| Conditional Statement | `if (.value.value greater_or_equal` 60)`` | 
{% /table %}

## Payload Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Severity | Error | 
| Message Style | Static | 
| Subject | High number of 5xx errors | 
{% /table %}