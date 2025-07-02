---
type: page
title: Throttle Processor
listed: true
slug: throttle-processor
description: 
index_title: Throttle Processor
hidden: 
keywords: 
tags: 
---

{% synced id="beta-banner" %}
{% /synced %}

## Description

The Throttle processor applies rate limiting to a stream of events to limit load on downstream destinations.

## Use

This processor is used for cases where a high-throughput of low-value events may be produced from a source, as a means of protecting destinations and services. The Throttle processor allows for granular rate limiting of events, either across the entire event stream or bucketed by the configured Key Field. Events that exceed the configured Limit within the time Window are discarded.

## Configuration

{% table widths="0,462" %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Limit | The number of events to allow during the time window. If you specify a **Key Field** , the limit will be applied to events for each unique value of that field. | 100 | 
| Window | The time window during which the configured limit is applied. Options include `Milliseconds`, `Seconds`, `Minutes`, and `Hours`. | 1min | 
| Key Field | When configured, the value from this field will be used to group events into separate buckets for throttling. If left blank, or if the event does not contain a value in this field, the event will be throttled as part of the default bucket. | `.app` | 
| Exclude | A conditional statement that will be applied to exclude events from throttling. | `if (.host equal 'host-4')` | 
{% /table %}

## Examples

### Limit Events by Field

This example shows a configuration that allows only 1 event every 1 second, for each unique value of the `.app`  field. Events produced by `host-4`  are excluded from throttling.

#### Before

{% code %}
{% tab language="json" title="json" %}
[
  {"host": "host-1", "app": "app-1", "message": "GET /server HTTP/1.1"},
  {"host": "host-1", "app": "app-1", "message": "POST /widgets/152 HTTP/1.1"},
  {"host": "host-2", "app": "app-1", "message": "GET /widgets HTTP/2"},
  {"host": "host-3", "app": "app-2", "message": "GET /widgets HTTP/2"},
  {"host": "host-3", "app": "app-2", "message": "PUT /widgets/5593 HTTP/1.1"},
  {"host": "host-4", "app": "app-2", "message": "GET /server/status HTTP/1.1"},  
]
{% /tab %}
{% /code %}

#### Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| Limit | 1 | 
| Window | 1s | 
| Key Field | `.app` | 
| Exclude | Field: `.host` \n\nOperator: `equal` \n\nValue: `host-4` | 
{% /table %}

#### After

Three events are produced - the first event in the stream for each unique value of `.app` , along with any events excluded from throttling (when `.host == "host-4"` ).

{% code %}
{% tab language="none" %}
{"host": "host-1", "app": "app-1", "message": "GET /server HTTP/1.1"}
{"host": "host-3", "app": "app-2", "message": "GET /widgets HTTP/2"}
{"host": "host-4", "app": "app-2", "message": "GET /server/status HTTP/1.1"}
{% /tab %}
{% /code %}