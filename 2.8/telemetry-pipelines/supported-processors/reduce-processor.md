---
type: page
title: Reduce Processor
listed: true
slug: reduce-processor
description: 
index_title: Reduce Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/reduce-pipeline-processor#description)

The Reduce processor takes multiple log input events and combines them into a single log event based on specified criteria.

## [Use](https://docs.mezmo.com/docs/reduce-pipeline-processor#use)

Reduce will combine many events into one over a window of time. **T**his is useful for retaining event fidelity, but eliminating unnecessary or duplicate fields that do not need to be stored.

Reduce can use one or more Group By fields to determine when to perform an operation. For example, you could use a `session_Id`  field value that is consistent across many event messages as criteria for putting those events into a single group to be merged. You may specify more than one Group By field, in which case each message with a unique combination of those field values opens a separate group of events to be merged together.

You can configure how fields are handled on a per-field basis with a merge strategy. If you don't specify the merge strategy, a **default** merge strategy for each reduced event follows this pattern:

- **String fields** - The first value is kept while successive ones are discarded
- **Number fields** - The values are summed, and that result becomes the value of the field

## [Configuration](https://docs.mezmo.com/docs/reduce-pipeline-processor#configuration)

There are three options to configure for this processor. Note that two of these can have any number of values specified.

{% callout type="info" title="Maximum Time Window" %}
The Reduce processor has a maximum window of 2 hrs or 7200000 milliseconds.
{% /callout %}

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| **Duration** | The total window of time over which to run the reduction | `3000ms (default)` | 
| **Group By** | The incoming event fields to group. If none are specified, all events are combined. | `.level` | 
| **Max Events** | The maximum number of events to collect before flushing the cache, even if the duration time has not been reached | `10` | 
| **Merge Strategy** | Determines how the contents of a specified field will be treated when added to the combined event. |  | 
{% /table %}

### [Merge Strategy Options](https://docs.mezmo.com/docs/reduce-pipeline-processor#merge-options)

The merge options define how the fields will be combined. Note that certain strategies require numeric values in order to function.

{% table %}
| Option | Description | Required Input Type | 
| ---- | ---- | ---- | 
| **Array** | Append each value to an array. | Any | 
| **Smallest Array** | Keep the shortest array detected | Array | 
| **Largest Array** | Keep the longest array detected. | Array | 
| **Unique Array** | Create an array of all unique values. | Any | 
| **Join with Space** | Concatenate each string value and separate with a space. | String | 
| **Join with New Line** | Concatenate each string value and add to a new line. | String | 
| **Join** | Concatenate each string value together with nothing between | String | 
| **Keep first** | Discard every value except the first one detected. | Any | 
| **Keep last** | Discard every value except the last one detected. | Any | 
| **Min Value** | Keep the smallest numeric value detected. | Numeric | 
| **Max Value** | Keep the largest numeric value detected. | Numeric | 
| **Sum** | Add all values together into a single summed value. | Numeric | 
{% /table %}

### Flush conditions

Flush conditions define the logical parameters to determine the start or stop of the Reducing behavior. Flush conditions work on the event context, so the conditions apply to the latest event received, not to the merged event.

{% table %}
| Option | Description | 
| ---- | ---- | 
| starts_when | Define the logical conditions on when to start reducing. Reduce will not start summarizing events until the conditions are achieved, and thereafter reduce based on the defined grouping conditions until the time window has been achieved. | 
| ends_when | Define the logical conditions on when to stop reducing and flush the buffer, egressing the summarized event so far. Reduce will stop summarizing the events for a specific group when the latest event matches the defined conditions. The reduce operation will stop before the maximum window time is reached. | 
{% /table %}

## Examples

### Reducing a firewall event

Given a typical AWS firewall TCP event, we want to summarize multiple event messages into a single message.

{% code %}
{% tab language="json" %}
{
  "az":"us-east-1b"
  "bytes":44
  "dest_ip":"10.1.3.81"
  "event_dest_port":17778
  "event_src_port":50813
  "name":"AWS-Network-Firewall-Multi-AZ-firewall"
  "pkts":1
  "proto":"TCP"
  "src_ip":"205.210.31.133"
  "tcp":{
  "flags":"02"
  "syn":true
 }
 "ts":"2023-06-13T22:31:41.163906+0000"
}
{
  "az":"us-east-1b"
  "bytes":44
  "dest_ip":"10.1.3.81"
  "event_dest_port":17778
  "event_src_port":50813
  "name":"AWS-Network-Firewall-Multi-AZ-firewall"
  "pkts":1
  "proto":"TCP"
  "src_ip":"205.210.31.133"
  "tcp":{
   "flags":"02"
   "syn":true
  }
 "ts":"2023-06-13T22:31:42.280321+0000"
}
{% /tab %}
{% /code %}

The group by conditions leverage the following fields:

1. `src_ip`
2. `src_port`
3. `dest_ip`
4. `dest_port`

The merge strategy:

- Retains the last timestamp `ts`, `event_dest_port`, `event_src_port`
- Keeps the unique array of the `tcp` values
- All other fields are using the default merge strategies, which sums the `bytes` and `packets`  and keeps the first values for all other strings

In this case the 2 events will be combined as follows with the default merge:

{% code %}
{% tab language="json" %}
{
  "az":"us-east-1b",
  "bytes":88,
  "dest_ip":"10.1.3.81",
  "event_dest_port":17778,
  "event_src_port":50813,
  "name":"AWS-Network-Firewall-Multi-AZ-firewall",
  "pkts": 2,
  "proto":"TCP",
  "src_ip":"205.210.31.133",
  "tcp":[
   {
    "flags":"02"
    "syn":true
   }]
 "ts":"2023-06-13T22:31:42.280321+0000"
}
{% /tab %}
{% /code %}