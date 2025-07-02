---
type: page
title: Sample Processor
listed: true
slug: sample-processor
description: 
index_title: Sample Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/sample-pipeline-processor#description)

The Sample processor filters incoming events at a specified rate. This reduces the total number of events that are used in a subsequent processor, or sent to a destination.

## [Use](https://docs.mezmo.com/docs/sample-pipeline-processor#use)

The Sample processor is useful when the number of events is in excess of the number required to understand the data. For instance, when determining performance metrics over time it's often sufficient to have one measurement per second rather than per millisecond.

## [Configuration](https://docs.mezmo.com/docs/sample-pipeline-processor#configuration)

The number of events for which a sample is set is computed based on an included rate number. The number of events forwarded is determined by the ratio 1/N, where N is the rate. The minimum sampling rate is 2, meaning every 1 of 2 events would be forwarded.

Data can be excluded from the sampling algorithm and always forwarded through the pipeline based on a conditional match of JSON key-value pairs. Data that matches the condition will always be retained.

### [Options](https://docs.mezmo.com/docs/sample-pipeline-processor#options)

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Rate | The rate at which events will be forwarded, expressed as 1/n. | `rate = 10` means 1 out of every 10 events will be forwarded and the rest will be dropped | 
| Always Include | Define a Field and conditions for log data to always be forwarded regardless of the Rate. |  | 
{% /table %}