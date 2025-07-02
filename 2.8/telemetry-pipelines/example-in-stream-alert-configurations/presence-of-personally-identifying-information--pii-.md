---
type: page
title: Presence of Personally Identifying Information (PII)
listed: true
slug: presence-of-personally-identifying-information--pii-
description: 
index_title: Presence of Personally Identifying Information (PII)
hidden: 
keywords: 
tags: 
---

This alert is triggered when the [auto$](/telemetry-pipelines/redact-processor) has the option `Mask PII Presence `set to `On` and a social security number, email address, or custom-defined pattern of PII is detected in the telemetry data. 

## General Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Name | PII Data Present | 
| Description | Triggers when the metadata field `pii_presence` contains a `yes` value for any of the pre-set or custom PII types. | 
{% /table %}

## Evaluation and Condition Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Operation |  | 
| Window Type |  | 
| Window Duration (minutes) |  | 
| Group by Field Paths |  | 
| Operation |  | 
| Window Type |  | 
| Window Duration |  | 
| Conditional Statement |  | 
| Event Timestamp |  | 
{% /table %}