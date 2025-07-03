---
type: page
title: Tutorial: Convert Events to Metrics
listed: true
slug: pipeline-example--convert-200-events-to-metrics
description: 
index_title: Tutorial: Convert Events to Metrics
hidden: 
keywords: 
tags: 
---


As described in the Mezmo Whitepaper "[auto$](/practioner-guide-data-optimization/optimize-your-observability-data-in-five-steps)," a simple way to reduce the overall volume of log data is to parse out routine messages, like `Status 200`messages, and then convert that data from events to metrics. Using this method, you can monitor these routine messages through a simple dashboard view, and then take action if you notice or are alerted to any anomalous spikes or decreases in these messages.

This topic describe a basic Pipeline architecture and Processor group for converting events to metrics that you can adapt to your own purposes, with examples of Processor configurations.

## Interactive Demo

You can see how data is processed and reduced through this Pipeline in this interactive version. You will need to have pop-ups enabled on your browser or for docs.mezmo.com to view the demo. You can [view the demo without a pop-up](https://www.mezmo.com/demos/event-to-metric-module) at mezmo.com.

{% html %}
&lt;!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page --&gt;
&lt;button data-navattic-open="https://capture.navattic.com/cluvrmmh700000fjs9ui3ei5e" data-navattic-title="Convert Events to Metrics "&gt;
View the demo in a pop-up
&lt;/button&gt;
{% /html %}

## Overview

This schematic of the Pipeline illustrates the Processor chain for converting 200 events to metrics. The Processor configurations are described in detail in the sections that match the numbers in the schematic.

{% image url="https://uploads.developerhub.io/prod/2KW7/0ov2u0zvukgzwvfd0vr1v2ylqe9u0o5ksmhp25xsebuv5ii7wpa2wciq4z6oc19o.png" caption="Overview of the architecture for a Pipeline that converts 200 events to metrics" mode="responsive" height="346" width="1518" %}
{% /image %}

## 1 - Demo/HTTP Source

Use the [HTTP Source](/telemetry-pipelines/http-source) to connect the Pipeline to your incoming telemetry data. The topic [Set Up and Test an HTTP Endpoint Source](/telemetry-pipelines/set-up-and-process-http-endpoint-data) includes tips and examples for configuring your source. This example uses the [auto$](/telemetry-pipelines/demo-logs-source) with the **JSON Logs** option to demonstrate the effects of the Processors on the data stream. You can also [try it out with a sample of your own data. ](/telemetry-pipelines/view-pipeline-data)

{% callout type="info" title="Try It with a Demo Source" %}
1. Log into the Mezmo App, and in the **Pipelines** section, click **New Pipeline**.
2. Add the **Demo Logs** Source, and for **Format**, select **JSON**.
3. Add the **Blackhole** Destination to your Pipeline, and connect it to the Demo Logs.
4. Add the Processors and their configurations as shown in this example.
5. To view the data transformations through the Processors, **Deploy** the Pipeline, and then click the **Tap** for the Source and each Processor to see the data as it egresses from each node. You will also be able to see how the data is reduced on the Pipeline Dashboard.

If you don't yet have a Mezmo account, you can [sign up for a 30 Day Free Trial](https://www.mezmo.com/sign-up-pipeline-today) to try us out!
{% /callout %}

## 2 - Route Processor

The [auto$](/telemetry-pipelines/route-processor) enables you to set conditions under which telemetry data will be sent to other points in the processing chain. In this case, it is set to send 200 events down the Processor Chain for conversion to metrics, while unmatched data is sent directly to the Destination. This example uses the Blackhole destination, where all data is dropped, but you could send matched and unmatched data to different destinations depending on your use case.

{% table widths="" %}

{% table %}
| Configuration Pameter | Setting | 
| ---- | ---- | 
| Conditional Statement for 200 Route | `if(.status equal 200)` | 
{% /table %}

{% /table %}

## 3 - Event to Metric Processor

The [auto$](/telemetry-pipelines/event-to-metric-processor) enables you implement a counter for the events sent to it, and attach tags to specified fields. In this case, the tags are sent to capture the values related to the URL and IP Address within the 200 event.

{% table widths="" %}

{% table %}
| Configuration Parameter | Setting | 
| ---- | ---- | 
| Metric Name | `number_hits` | 
| Kind | `Incremental` | 
| Type | `Counter` | 
| Type/Value Type | `New Value` | 
| Type/Value | `1` | 
| Type/Namespace/Value Type | `None` | 
| Tag 1/Name | `url` | 
| Tag 1/Value Type | `Value from event field` | 
| Tag 1/Field Value | `.host` | 
{% /table %}

{% /table %}

## 4 - Aggregate Metrics Processor

The final Processor in the chain, the [auto$](/telemetry-pipelines/aggregate-processor) aggregates multiple metric events into a single metric based on a defined time interval. In this case, it aggregates the value of the 200 metrics over a 10 second interval into a single number.

{% table widths="" %}

{% table %}
| Configuration Parameter | Setting | 
| ---- | ---- | 
| Interval | `10 seconds` | 
{% /table %}

{% /table %}

## 5 - Blackhole Destination

The [auto$](/telemetry-pipelines/blackhole-destination) Destination drops all data sent to it. This makes it useful for testing your Processor chain to make sure you are getting the expected results before sending them on to a production destination. Mezmo supports a wide variety of popular destinations including [auto$](/telemetry-pipelines/mezmo-destination), [auto$](/telemetry-pipelines/datadog-metrics-destination), and [auto$](/telemetry-pipelines/prometheus-remote-write-destination).

## For More Information

For more information on how to understand and optimize your telemetry data, [contact our Solutions Engineering team](https://go.mezmo.com/mezmo-data-profiling?_gl=1*189zkyo*_ga*NDQxOTc0Mzg1LjE2NDE0MTYxODc.*_ga_C3EJ23NJFV*MTcxMTU3ODkyNi45OC4xLjE3MTE1Nzg5MzIuMC4wLjA.)  to schedule a free consultation.