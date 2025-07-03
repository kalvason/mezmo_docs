---
type: page
title: Trace Sampling Processor
listed: true
slug: trace-sampling-processor
description: 
index_title: Trace Sampling Processor
hidden: 
keywords: 
tags: 
---


## Description

Performs sampling of traces per a given rate using the Trace ID as the unique identifier. If a trace is rate selected, all spans of the trace are output.

{% synced id="experimentalbanner" %}
{% /synced %}

## Use

Two well-known optimization techniques for traces are Deterministic Sampling (Head sampling) and more advanced Tail-based sampling. While head-based sampling will treat all traces equally and sample randomly, Tail-based sampling enables you to sample at different rates for traces you consider to have different levels of importance, based on attributes that traces contain, for example prioritizing traces with errors, latency, or traces that exceed certain performance thresholds. This is implemented in this Processor through conditional statements to define the trace.

{% callout type="info" title="OTel Only" %}
This Processor supports sampling of [OTel traces only](https://opentelemetry.io/docs/concepts/signals/traces/).
{% /callout %}

## Configuration

{% table widths="" %}

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Sample Type | The type of sampling to invoke. | `head`  `tail` | 
| Trace ID field | The field to use as the identifier of a trace. | `.context.trace_id` | 
| Rate | The rate at which to sample traces. For example, `10` means 1 out of every 10 traces will be sampled. | `10` | 
| Parent Span ID (Tail Only) | The field to use as the parent span identifier. | `.parent_span_id` | 
| Conditional (Tail Only) | Used in conjunction with Rate, a conditional statement to define the field for sampling |  | 
{% /table %}

{% /table %}

## Examples

Examples of OTEL traces that can be sampled using the Processor.


#### The head of a trace indicated by a null parent_id field

{% code %}
{% tab language="json" %}
{
"name": "hello",
"context": {
"trace_id": "5b8aa5a2d2c872e8321cf37308d69df2",
"span_id": "051581bf3cb55c13"
},
"parent_id": null,
"start_time": "2022-04-29T18:52:58.114201Z",
"end_time": "2022-04-29T18:52:58.114687Z",
"attributes": {
"http.route": "some_route1"
},
"events": [
{
"name": "Guten Tag!",
"timestamp": "2022-04-29T18:52:58.114561Z",
"attributes": {
"event_attributes": 1
}
}
]
}
{% /tab %}
{% /code %}


#### A related span under the same trace, indicated by the parent_id matching the span_id of the head

{% code %}
{% tab language="json" %}
{
"name": "hello-salutations",
"context": {
"trace_id": "5b8aa5a2d2c872e8321cf37308d69df2",
"span_id": "93564f51e1abe1c2"
},
"parent_id": "051581bf3cb55c13",
"start_time": "2022-04-29T18:52:58.114492Z",
"end_time": "2022-04-29T18:52:58.114631Z",
"attributes": {
"http.route": "some_route3"
},
"events": [
{
"name": "hey there!",
"timestamp": "2022-04-29T18:52:58.114561Z",
"attributes": {
"event_attributes": 1
}
}
]
}
{% /tab %}
{% /code %}