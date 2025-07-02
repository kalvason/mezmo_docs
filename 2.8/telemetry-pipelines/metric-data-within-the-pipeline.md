---
type: page
title: The Pipeline Metric Data Model
listed: true
slug: metric-data-within-the-pipeline
description: 
index_title: The Pipeline Metric Data Model
hidden: 
keywords: 
tags: 
---

## Introduction

The Mezmo Telemetry Pipeline platform enables you to quickly and easily process metrics within your pipeline using out-of-the-box functionality. This includes support for use cases such as:

- Extracting metrics embedded in logs to be sent downstream with the [auto$](/telemetry-pipelines/parse-processor)
- [Aggregating](/telemetry-pipelines/aggregate-processor) metric values to reduce storage needs
- [Limiting tag cardinality](/telemetry-pipelines/metrics-tag-cardinality-limit-processor) to limit downstream load and preserve stability within metric storage systems

Metrics within the Telemetry Pipeline are handled in the same way that log events are handled, with the exception that certain Processors require the events to be in a specific format in order to function.

Metric values from supported metric Sources, such as [Prometheus](/telemetry-pipelines/prometheus-remote-write-source), are automatically created with the appropriate format to be used within any pipeline. They will also be automatically compatible with any downstream Destinations, such as [auto$](/telemetry-pipelines/prometheus-remote-write-destination) and [auto$](/telemetry-pipelines/datadog-metrics-destination).

If you have metrics that are not properly formatted, you can use the [auto$](/telemetry-pipelines/event-to-metric-processor) to transform them into the appropriate model for subsequent processing and sending downstream.

## The Metric Data Model

Metric data within the Pipeline must follow a standard format in order to be used in any processors or destinations that require a metric value.

This table describes the data model for various fields, including the data type for the field, and whether it is required for the data model. 

{% table widths="108,0,0" %}
| Field | Data type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| `name` | String | Yes | The name for the metric | 
| `kind` | Enumerated set | Yes | The type of metric, either `incremental` or `absolute` | 
| `value` | Object | Yes | An object of the classes `gauge` , `counter` , `distribution`, `set`, `histogram`, or `summary` | 
| `namespace` | String | No | An optional value for distinguishing metric values with the same name | 
| `tags` | Object | No | An optional set of tag keys and values | 
{% /table %}

This code block is a JSON representation of the metric model with example values:

{% code %}
{% tab language="json" title="counter" %}
{
  "name": "go_goroutines",
  "namespace": "myspace",
  "tags": {
    "instance": "host-address:443"
  },
  "kind": "absolute",
  "value": {
    "type": "counter",
    "value": 36
  }
}
{% /tab %}
{% tab language="json" title="gauge" %}
{
  "name": "go_goroutines",
  "namespace": "myspace",
  "tags": {
    "instance": "host-address:443"
  },
  "kind": "absolute",
  "value": {
    "type": "gauge",
    "value": 55.3
  }
}
{% /tab %}
{% tab language="json" title="set" %}
{
  "name": "my_set",
  "namespace": "myspace",
  "tags": {
    "instance": "host-address:443"
  },
  "kind": "absolute",
  "value": {
    "type": "set",
    "value" : {
        "values": ["apple", "orange", "pear"]
    }
  }
}
{% /tab %}
{% tab language="json" title="histogram" %}
{
  "name": "my_histogram",
  "namespace": "myspace",
  "tags": {
    "instance": "host-address:443"
  },
  "kind": "absolute",
  "value": {
    "type": "histogram",
    "value": {
        "buckets" : [
            {
                "upper_limit": 5000,
                "count": 70
            },
            {
                "upper_limit": 1000,
                "count": 30
            }
        ],
        "count": 100,
        "sum": 4500
    }
  }
{% /tab %}
{% tab language="json" title="distribution" %}
{
  "name": "my_dist",
  "namespace": "myspace",
  "tags": {
    "instance": "host-address:443"
  },
  "kind": "absolute",
  "value": {
    "type": "distribution",
    "value": {
        "samples" : [
            {
                "value": 5000,
                "rate": 90
            },
            {
                "value": 1000,
                "rate": 40
            }
        ],
        "statistic": "histogram"
    }
  }
}
{% /tab %}
{% tab language="json" title="summary" %}
{
  "name": "my_summary",
  "namespace": "myspace",
  "tags": {
    "instance": "host-address:443"
  },
  "kind": "absolute",
  "value": {
    "type": "summary",
    "value": {
        "quantiles" : [
            {
                "quantile": 0.5,
                "value": 70
            },
            {
                "quantile": 0.73,
                "value": 90
            }
        ],
        "count": 90,
        "sum": 4500
    }
  }
}
{% /tab %}
{% /code %}

## Transforming Metrics

There are multiple ways to transform data to create or manipulate a metrics event. Keep in mind the metric event is treated as a log until it is an input to a metrics processor, or sent to a metric destination.

1. You can use all of the standard processors, such as **Drop Fields**, **Filter**, and **Route** on any metrics, so long as none of the required fields are removed.
2. You can use the [auto$](/telemetry-pipelines/event-to-metric-processor) to directly transform any log input into a metric format event at exit. However, you cannot create a `histogram`, `distribution`, `set` or `summary` using this processor
3. You can use the [auto$](/telemetry-pipelines/map-fields-processor) to move data within an event so that it matches the metric data mode. This requires all of the metric fields to be present already and parsed
4. You can use the [auto$](/telemetry-pipelines/parse-processor) to extract all of the necessary fields to match the metric data model.

{% callout type="info" title="Use Event to Metric Processor for HTTP or Log Sources" %}
If you use an HTTP Source or extract a metric from a log, you will need to use the [auto$](/telemetry-pipelines/event-to-metric-processor) or another suitable method to make sure the metric data is formatted to match the Mezmo metrics model.
{% /callout %}