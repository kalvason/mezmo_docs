---
type: page
title: Aggregate Processor
listed: true
slug: aggregate-processor
description: 
index_title: Aggregate Processor
hidden: 
keywords: 
tags: 
---

## Description

With the Aggregate Processor you can aggregate metrics and events for specified fields, and then evaluate those aggregations using defined conditions to send alerts when those conditions are met. 

## Use

Evaluate Metric or Log event fields using any aggregation strategy such as Sum, Average, Min, or Max and trigger alerts based on specified conditions.

{% callout type="info" title="Tumbling v. Sliding Windows" %}
**Tumbling** windows are a series of fixed-sized, non-overlapping and contiguous time intervals. For example, if you set it to a five-minute tumbling window, the elements with timestamp values [0:00:00-0:05:00) are in the first window. Elements with timestamp values [0:05:00-0:10:00) are in the second window.

A S**liding** window has a fixed time length, and it moves forward or “slides” at a time interval smaller than the window’s length. For example, a sliding window can be five minutes long, and slide every one minute and capture five minutes of data. The length of the slide is not user-configurable by user, the system will automatically calculate an appropriate slide based on the window size.
{% /callout %}

{% callout type="info" title="Limits on Processor Inputs" %}
Each Processor input to the Aggregate Processor is a single thread. Inputs from three or more Processors can result in slower processing times.
{% /callout %}

{% table widths="94,0" %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Group By | Select one or more field names. The processor aggregates the data based on a unique set of field values. \n\nUses the **Name**, **Namespace**, and **Tag** fields for the grouping. | .app or .tags.cluster | 
| Evaluate | Choose the evaluation method for the fields. Note that these evaluation methods only apply to `metrics`. For `logs`, you will need to create a custom evaluation method. \n\n\n\n- Add\n- Sum\n- Minimum\n- Maximum\n- Average\n- Set intersection\n- Distribution cocantenation\n- Custom |  | 
| Window Type | - Tumbling\n- Sliding | Sliding | 
|  | Tumbling &#124; Interval in seconds\n\n\n\nRange: 1 minute to 25 hours | 1800 | 
|  | Sliding &#124; Interval | 1800 | 
|  | Sliding &#124; Minimum Duration | 180 | 
| Condition | The conditions to trigger an Alert based on aggregated/evaluated value. Two types of alerting are supported: |  | 
|  | **Threshold Alert**\n\n\n\nCompare the aggregated value to a specified threshold value.\n\n\n\nComparison operators:\n\n\n\n`greater`\n\n\n\n`greater_or_equal`\n\n\n\n`less`\n\n\n\n`less_or_equal` | `.value.value <greater_or_ equal_to> 90` | 
|  | **Change Alert** \n\n\n\nSet conditions based on how much the aggregated value changed compared to the prior evaluation. This change can be based on % change or absolute value change.\n\n\n\nPercent change operators:\n\n\n\n`percent_change_greater`\n\n\n\n`percent_change_greater_or_equal`\n\n\n\n`percent_change_less`\n\n\n\n`percent_change_less_or_equal`\n\n\n\nValue change operators:\n\n\n\n`value_change_greater`\n\n\n\n`value_change_greater_or_equal`\n\n\n\n`value_change_less_or_equal` | `.value.value <percent_change_greater> 50`\n\n\n\n`.value.value <value_change_greater> 200` | 
{% /table %}

## Custom Option

If the event isn't an OTEL metrics event (for example, the metric value is not in the path .value.value), you can aggregate the value with custom aggregation logic based on Mezmo's JavaScript framework. The topic for the [Script Execution Processor](https://docs.mezmo.com/telemetry-pipelines/js-script-processor#configuration) provides more details about Mezmo’s JavaScript framework. 

For example, if you are looking to sum the `error_count` property of all log events, you would use this script:

{% code %}
{% tab language="javascript" %}
function aggregateEvent(accum, event, metadata, annotations) {
   accum.error_count = accum.error_count + event.error_count
   return accum  
}
{% /tab %}
{% /code %}

With a Custom aggregation strategy, it is important to note that the initial value of the `accum` object is **the first event in the window** . Your script will only be executed for subsequent events in the window. Each time the script is executed within the window, it will be called with the previous value of `accum`  and the current `event` . When the window elapses, the value of `accum`  will be emitted as the aggregated event.

For example, if you are looking to aggregate a count of events into a **new field:**

{% code %}
{% tab language="javascript" %}
function aggregateEvent(accum, event, metadata, annotations) {
  // The first time this script is executed will be on the second
  // event in the window, with `accum` representing the first event.
  //
  // Initialize a new field on `accum`, setting it to
  // 1 to represent the fact that 1 event is already present
  // in the buffer
  if (!accum.event_count) {
    accum.event_count = 1
  }

  // Now that we've accounted for the accum event and initialized
  // the new field with a value, we can add 1 to the current count.
  accum.event_count = accum.event_count + 1
  return accum
}
{% /tab %}
{% /code %}

## Metadata Fields

The Aggregate Processor rocessor adds these metadata fields when an event is emitted. 

{% table widths="" %}
| Metadata Field |  | 
| ---- | ---- | 
| .metadata.aggregate.flush_timestamp | The time when the Processor emitted the aggregation event. This could be due to the following:\n\n\n\n- Window time has been completed\n- Triggered by the condition | 
| .metadata.aggregate.start_timestamp | Aggregation window start time | 
| .metadata.aggregate.end_timestamp | Aggregation window end time | 
| .metadata.aggregate.event_count | # of events aggregated | 
{% /table %}

### Detecting Alert vs Aggregation Output

 You can use these fields to determine if the event is triggered due to a threshold breach or a normal aggregation event.

An alert is triggered if 

{% code %}
{% tab language="none" %}
.metadata.aggregate.flush_timestamp < .metadata.aggregate.end_timestamp
{% /tab %}
{% /code %}

Normal Aggregation Event if

{% code %}
{% tab language="none" %}
.metadata.aggregate.flush_timestamp > =  .metadata.aggregate.end_timestamp
{% /tab %}
{% /code %}