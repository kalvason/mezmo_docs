---
type: page
title: Percentage Volume Increase
listed: true
slug: percentage-volume-increase
description: 
index_title: Percentage Volume Increase
hidden: 
keywords: 
tags: 
---


This is an example of an alert that is triggered when there is an increase in the volume of data beyond a set percentage.

## General Configuration

{% table %}

{% table %}
| Field | Value | 
| ---- | ---- | 
| Name | Volume increase by 40% | 
| Description | Alert when volume increases by 40% compared to the prior period | 
{% /table %}

{% /table %}

## Evaluation and Condition Configuration

{% table %}

{% table %}
| Field | Value | 
| ---- | ---- | 
| Alert Type | Change Alert | 
| Event Type | Metric | 
| Group by Field Paths | `.name` `.namespace` `.tags` | 
| Operation | Sum | 
| Window Type | Tumbling | 
| Window Duration (minutes) | 15 | 
| Alert Conditions | `if (.value.value` `percent_change_``greater_or_equal 40)` | 
{% /table %}

{% /table %}

## Payload Configuration

{% table %}

{% table %}
| Field | Value | 
| ---- | ---- | 
| Severity | Warning | 
| Message Style | Static | 
| Subject | Volume Surge at [name of Source] | 
{% /table %}

{% /table %}