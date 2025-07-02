---
type: page
title: Sudden Increase in Source Volume
listed: true
slug: sudden-increase-in-source-volume
description: 
index_title: Sudden Increase in Source Volume
hidden: 
keywords: 
tags: 
---

This alert is triggered when there is a 60% increase in data volume compared to a prior window. 

## General Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Name | Sudden increase in source volume. | 
| Description | Triggers when a source volume increases by 60% compared to prior window. | 
{% /table %}

## Evaluation and Condition Configuration

{% table %}
| Field | Value | 
| ---- | ---- | 
| Operation | Custom | 
| Window Type | Tumbling | 
| Window Duration (minutes) | 30 | 
| Group by Field Paths | `.source` | 
| Operation | Custom | 
| Window Type | Tumbling | 
| Window Duration (minutes) | 30 | 
| Conditional Statement | `if (.log_volume`percent_change`_greater_or_equal 60)` | 
| Event Timestamp | `.timestamp` | 
{% /table %}

## Custom Script

{% code %}
{% tab language="bash" %}
// Receives the current event, metadata and an accumulator object. Logic can be performed
// on the event properties and added to the accumulator object for later analysis.
// The accumulator is persisted, and will become the emitted event when
// conditions are true, OR if the time window naturally expires. Those same conditions
// will also be evaluated against the emitted event to determine if the alert should
// be triggered.

function alertAggregation(accum, event, metadata) {
  let new_accum = accum
  if (!new_accum.message.log_volume) {
    const accum_str = JSON.stringify(accum)
    const accum_length = accum_str.length
    new_accum = {message: {log_volume: accum_length}}
  }
  
  const event_str = JSON.stringify(event)
  const event_length = event_str.length
  new_accum.message.log_volume = new_accum.message.log_volume + event_length
  
  return new_accum
}
{% /tab %}
{% /code %}