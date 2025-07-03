---
type: page
title: Aggregate Processor DEPRECATE
listed: false
slug: aggregate-processor-deprecate
description: 
index_title: Aggregate Processor DEPRECATE
hidden: 
keywords: 
tags: 
---

## Description

The Aggregate processor combines multiple metric events into a single metric event based on the type. This reduces the total size needed to store the metric events for a specified time interval.

## Use

Metric data can have more data points than needed to understand the behavior of a system. Excess metrics can lead to a higher cost of storage without an increase in value.

For example, you may have metrics being sent on a 1 millisecond basis, while having metrics on a 1 second basis would suffice for a particular measurement. Rather than storing 1000 data points, the Aggregate processor can combine those into a single metric data point.

{% callout type="info" title="Time Window for Aggregation" %}
Aggregation occurs as the metrics come in. While some metrics have a timestamp, metrics are processed when they are received.

Late metrics will be aggregated with current metrics.
{% /callout %}

### Metric Types

#### Incremental

Incremental metric values, such as counters or sums, are added together when aggregating.

For example, an incremental counter of 5 and an incremental counter of 10 would yield an aggregated value of 15.

#### Absolute (Gauge)

Absolute values are not additive. Newer values will replace older values. Effectively this can be thought of as "last sampled value" within a series.

For example, a gauge with a value of 120 followed by a gauge with a value of 129 will yield an aggregated value of 129.

#### Complex types

Complex types include histograms, sets, distributions and summaries. These types are added together similar to incremental types.

### Names, Namespaces, and Tags

Metrics are aggregated when their names, namespaces, and tags are the same. If their namespaces or tags are different, they will be grouped and aggregated for that unique set.

Should you wish to aggregate across metrics with different tags, drop those fields prior to the Aggregate processor to ensure they are summarized as desired.

## Configuration

The only configuration option is the length of time during which the aggregation is to be performed in milliseconds. Type recognition is handled automatically within the live stream.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Interval | The number of milliseconds over which the aggregation window will run | 1000 ms | 
{% /table %}

## Examples

### Aggregating an incremental metric

Incremental metrics are "summable" to allow for aggregating individual values over the specified time period. In this example, we will show adding a set of metrics using the Aggregate processor.

#### Before

The metric measurements are spread over a 1 ms time period. We will only be summing for 3 time periods in this example, meaning the interval is far greater than the length needed.

{% code %}
{% tab language="json" %}
{
  "kind":"incremental",
  "name":"bucket_cache_count",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 300
  }
}
{
  "kind":"incremental",
  "name":"bucket_cache_count",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 301
  }
}
{
  "kind":"incremental",
  "name":"bucket_cache_count",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 283
  }
}
{% /tab %}
{% /code %}

#### Options

We'll set the aggregation window to 1 second.

{% table %}
| Option | Value | 
| ---- | ---- | 
| Interval | 1000 | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{
  "kind":"incremental",
  "name":"bucket_cache_count",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 884
  }
}
{% /tab %}
{% /code %}

### Aggregating an absolute metric

Absolute metrics are not summable. This means that to aggregate them leverages taking the final value of a set and using that as the representative value for the whole set.

#### Before

{% code %}
{% tab language="json" %}
{
  "kind":"absolute",
  "name":"memory_usage_k8s_compapp",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 520032
  }
}
{
  "kind":"absolute",
  "name":"memory_usage_k8s_compapp",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 564321
  }
}
{
  "kind":"absolute",
  "name":"memory_usage_k8s_compapp",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 547679
  }
}
{% /tab %}
{% /code %}

#### Options

We'll set the aggregation window to 1 second. This means the last value to be sent within the interval is recorded as the absolute metric.

{% table %}
| Option | Value | 
| ---- | ---- | 
| Interval | 1000 | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{
  "kind":"absolute",
  "name":"memory_usage_k8s_compapp",
  "namespace":"k8s_prod_set1",
  "tags": {
    "environment":"prod",
    "pod":"pod01",
    "source":"prometheus_collector"
  },
  "value":{
    "type":"counter",
    "value": 547679
  }
}
{% /tab %}
{% /code %}