---
type: page
title: Pipeline Example: Trigger Alerts with Metric Data
listed: false
slug: trigger-alerts-metric-data
description: 
index_title: Pipeline Example: Trigger Alerts with Metric Data
hidden: 
keywords: 
tags: 
---


This topic describes a typical use of the [auto$](/telemetry-pipelines/event-to-metric-processor) in a Mezmo Telemetry Pipeline, and provides an architectural template to use in designing Pipelines for the purpose of triggering alerts with log data.

## The Scenario

This example illustrates a scenario in which you want to monitor some type of event, in this case credit card transactions, and trigger an alert when the number of events reaches a set threshold during a defined interval of time.

To accomplish this, you need to use the [auto$](/telemetry-pipelines/event-to-metric-processor) to convert the transaction events to a Count metric, followed by an [auto$](/telemetry-pipelines/aggregate-processor-deprecate) that will aggregate those events over 30 second intervals. A [auto$](/telemetry-pipelines/route-processor) at the end of the chain sends events meeting the match criteria to an [auto$](/telemetry-pipelines/http-destination)/WebHook Destination that will send the alert, while routing all transaction data to a [auto$](/telemetry-pipelines/prometheus-remote-write-destination)/Grafana instance for further analysis.

You can adapt this template to your own needs by building the Pipeline shown here, and changing the configuration settings in each of the Processors to match the events, thresholds, and Destinations that are appropriate to your situation.

## Architecture Overview

{% image url="https://uploads.developerhub.io/prod/2KW7/5tqns3bdxo1ekvxq9iufknr68np69r6aaguacvgonjzyv6lngex1xmptrtfbtsmo.png" caption="The Event to Metric Pipeline" mode="responsive" height="358" width="1484" %}
{% /image %}

### 1 Sources

The Source for this Pipeline uses sample financial data from the [auto$](/telemetry-pipelines/demo-logs-source) to model the events that will be processed, but you could a demo log Source for any type of event data that you want to use to trigger an alert.

{% callout type="success" title="Demo Source Best Practice" %}
During the Pipeline design process, you should use a demo log source to make sure your data is being processed as intended before you connect it to a production Source. The topic [auto$](/telemetry-pipelines/simulate-pipeline-data-flows) has more information on how to build and test a Pipeline using demo Sources and samples.
{% /callout %}

You can view the sample data for a demo Source by clicking on the Source node in the map, then select **Tap Egress**. You can also download the sample data to view the full JSON, and [and build your own sample data.](/telemetry-pipelines/view-pipeline-data)

{% image url="https://uploads.developerhub.io/prod/2KW7/focpdqfpv5i7zm52tqlpw8j5ppwgedgmuacm319ndscwk39j1zfjfarjh8nzjpx0.png" caption="The unprocessed data for the financial data demo Source" mode="600" height="572" width="713" %}
{% /image %}

### 2 Filter Processor

The first step in this Pipeline is to use the [auto$](/telemetry-pipelines/filter-processor) to remove any events from the data stream that are not `transaction` events. In this case, the conditional statement within the filter is set to match those events, and then allow them to pass through the filter.


#### Configuration

{% table %}

{% table %}
| Setting | Parameter | 
| ---- | ---- | 
| **Action** | `Allow events matching this criteria` | 
| **Conditional Statement** | `if(exists(.transaction))` | 
{% /table %}

{% /table %}

To make sure that the filter is processing the data as intended, you can again use the **Tap Egress** feature to compare the source data with the filtered data.

{% image url="https://uploads.developerhub.io/prod/2KW7/k2j9rl77v0484q54a0ffgyd67dytaugiauy3sl9l6e8oviv7azd8fkmr0jiz0b8e.png" caption="The filtered Source data" mode="600" height="1184" width="1440" %}
{% /image %}

### 3 Event to Metric Processor

With the data stream filtered so that only transaction events are included, the next step is to convert the events to a metric that can be aggregated. In this case, the Processor is set to create an incremental counter metric for card authorization events, and tag them as authorized or denied based on the value of the `transaction.result_reason`field.


#### Configuration

{% table widths="148,147,0,0" %}

{% table %}
| Setting | Secondary Setting | Tertiary Setting | Parameter |  | 
| ---- | ---- | ---- | ---- | ---- | 
| **Metric Name** |  |  | `card_authorization_count` |  | 
|  | **Kind** |  | `Incremental` |  | 
| **Type** |  |  | `Counter` |  | 
|  | **Value** |  |  |  | 
|  |  | **Value type** | `New value` |  | 
|  |  | **Value** | `1` |  | 
|  | **Namespace** |  |  |  | 
|  |  | **Value type** | `None` |  | 
|  | **Tags** |  |  |  | 
|  |  | **Name** | `card_authorization` |  | 
|  |  | **Field value** | .`transaction.result_reason` |  | 
|  |  | **Value type** | `Value from event field` |  | 
{% /table %}

{% /table %}

{% image url="https://uploads.developerhub.io/prod/2KW7/fj5tgmwbweb7o0reyb8k0we62wy2yl1l5f79oy7sw0m2o6y7fuvoyaeob4hxeww0.png" caption="Transaction events converted to metrics" mode="600" height="646" width="921" %}
{% /image %}

### 4 Aggregate (Metrics) Processor

The [auto$](/telemetry-pipelines/aggregate-processor-deprecate) aggregates multiple metric events into a single metric event based on a defined interval window. In this case, the Processor aggregates the `card denied` and `card authorized` transaction events to the number counted in a 30 second interval.


#### Configuration

{% table %}

{% table %}
| Setting | Parameter | 
| ---- | ---- | 
| **Interval** | `30000` | 
{% /table %}

{% /table %}

{% image url="https://uploads.developerhub.io/prod/2KW7/32fqbxhjs6xihn0mbxinjdagj4difs4pj7ie7la1tdazrj8bxy1x9daqwvx19v2c.png" caption="Aggregated transaction events" mode="600" height="639" width="934" %}
{% /image %}

### 5 Route Processor

The [auto$](/telemetry-pipelines/route-processor) uses conditional statements to send processed metrics to Destinations for storage and analysis. In this case, there are two routes:

1. When the count of `card_denied` events reaches 5 or more in a 30 second interval, those events are routed to an HTTP endpoint that triggers an alert.
2. All events are routed to Prometheus Remote Write - Grafana instance for storage and further analysis.

{% table %}

{% table %}
| Route Name | Purpose | Conditional Statement |  | Routed To | 
| ---- | ---- | ---- | ---- | ---- | 
| All Events | Sends all events to Prometheus Remote Write - Grafana instance | `if (exists(.))` |  | Prometheus Remote Write/Grafana | 
| Unmatched | Sends any data or metrics that don't match the other routing criteria to the Black Hole Destination. | None |  | Black Hole | 
| Card Denied &gt; 5 | Sends `card_denied` events to an HTTP endpoint to trigger an alert when the count of those events equals or exceeds 5 during a 30 second interval | `if (.tags.card_authorization equal 'card denied' AND .value.value greater` or_equal 5)`` |  | HTTP Endpoint/Webhook | 
{% /table %}

{% /table %}

### 6 Destinations

This Pipeline terminates with three Destinations:

1. A Grafana - Prometheus Remote Write instance, where all the transaction data is sent for additional analysis.
2. A Webhook HTTP Endpoint where the `card_denied` events are routed to trigger an alert.
3. A Black Hole destination for removal of extraneous data and events that don't match any of the criteria in the Route Processor.

{% image url="https://uploads.developerhub.io/prod/2KW7/sokcals2v4fgnhp8nn572h2yv80ldtp5zki47w950yl4a1ekf1s871wbq8cv9wpe.png" caption="Webhook for card_denied alert" mode="full" height="570" width="1182" %}
{% /image %}