---
type: page
title: Event to Metric Processor
listed: true
slug: event-to-metric-processor
description: 
index_title: Event to Metric Processor
hidden: 
keywords: 
tags: 
---

## Description

This processor provides an easy way to create a new metric event within the pipeline, typically from an existing log message. The new metric event can use data from the log to generate the metric, including the value if desired.

## Use

Log messages may contain embedded metrics that can be used in downstream alerting or analysis. However, extracting the metric from the log and putting it into a metric format can be a challenge.

This processor has predefined fields to build a new metric event from a log message. You could also use it to transform an existing metric event if needed.

The output of this processor is allowed to be one of the following types:

1. Counter
2. Sum
3. Gauge

The data model corresponds to the [Mezmo metric data model](/telemetry-pipelines/metric-data-within-the-pipeline).

{% callout type="warning" title="Input Event Dropped" %}
This processor drops the input event and outputs the metric event. If you want to keep the original event, wire it in parallel to another destination or processor.
{% /callout %}

## Configuration

The configuration of this processor corresponds directly to the metric data model. Many of the values could be taken from the original event or from user given static values within the processor itself.

{% table widths="" %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Metric Name | The name you want to give the metric, without spaces | `Error_count` | 
| Kind | The kind of metric this event represents, either `incremental` or `absolute` | `incremental` | 
| Type | Can be a sum, counter, or gauge | Counter | 
| Value | The numeric value of the metric. Can be provided as a static or a field reference from within the incoming event. | 42 | 
| Namespace | The namespace to give the metric. Can be provided as a static or a field reference from within the incoming event. | `.env` | 
| Tag Field | Tag names to be added. More than one can be defined. Can be provided as a static or a field reference from within the incoming event. | `app` | 
| Tag Value | The value to include for the tag. Can be provided as a static or a field reference from within the incoming event. | `prod` | 
{% /table %}

## Interactive Demo

Check out an interactive demo of the Event to Metric Processor as a component in of [an event to metric conversion Processor Group](/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics), as well as instructions for building a version of the Pipette with your own sample data in the topic [Tutorial: Convert Events to Metrics](https://docs.mezmo.com/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics).  You will need to have pop-ups enabled to view the demo, or you can [view it without a pop-up](https://www.mezmo.com/demos/event-to-metric-module) at mezmo.com. 

{% html %}
<!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page -->
<button data-navattic-open="https://capture.navattic.com/cluvrmmh700000fjs9ui3ei5e" data-navattic-title="Convert Events to Metrics ">
  View the demo in a pop-up
</button>
{% /html %}