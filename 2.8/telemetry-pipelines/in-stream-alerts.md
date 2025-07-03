---
type: page
title: In-Stream Alerts
listed: true
slug: in-stream-alerts
description: 
index_title: In-Stream Alerts
hidden: 
keywords: 
tags: 
---

Mezmo offers two methods for setting in-stream alerts for Pipeline data:

1. With the [auto$](/telemetry-pipelines/aggregate-processor),  you can set alerts that will trigger based on specific conditions for both metrics and events that pass through the Processor within the Pipeline. 
2. You can set also set in-stream alerts based on specific conditions for telemetry data on any Source or Processor in your Pipeline, as described in the topic [auto$](/telemetry-pipelines/set-in-stream-alerts). In this approach, alerting complexity is abstracted and makes it easy for you to configure alerts and also define message template for notification of alerts. Since alerting is part of any pipeline node, your pipeline complexity is hidden and easy to manage. 

With both options, you can use also use the alerts to trigger a [Responsive Pipeline](/telemetry-pipelines/configure-responsive-pipelines), but only node-specific alerts will trigger email or other types of notifications.

## Use Cases

**Benefits of Alerting in Pipeline**

Alerts that are triggered from within an observability platform are typically sent "after the fact" - that is, the log data that triggers the alert has already been indexed, and queries are run periodically against this indexed data to detect alerts. This means that there is always a few minutes of latency in detecting and notifying the alerts in the Observability tool. In addition, alerting in Observability platforms is limited to Indexed data only, meaning that low value data is often directly sent to low-cost cloud storage, and unusual trends in this data can go undetected.

In-stream alerts, in contrast, execute their queries for trigger conditions on the data stream within a Pipeline, so the latency between a trigger condition being met and alert being sent is typically measured in seconds. And unlike observability platform alerts, which can only be set on metrics,  in-stream alerts can be set for both metrics and logs. This means that you can design your Pipeline to be responsive to alert conditions as they happen. 

With in-stream alerts, you can:

- Reroute, throttle, or sample data if the data from a specific source or application suddenly surges
- Detect important signals prior to archiving/dropping occasionally used logs
- Detect increasing service errors, for example `HTTP 5xx` errors, for granular service paths within a few seconds
- Detect increasing trends in error messages per App, Host, or any service dimension,  to switch the Pipeline functionality to **Incident Mode**
- Run real-time health checks on Sources and Destinations for unusually low volume or missing health check events

In-stream alerts on Pipeline data provide a low-cost opportunity to analyze and detect important signals before data gets optimized and routed to its destinations.

## Alert Conditions

For both alert types, there are three types of alert conditions that you can set.

{% table widths="" %}
| Alert Type | Description | 
| ---- | ---- | 
| Threshold Alert | If the alert conditions meet, exceed, or fall below a set threshold value, an alert is triggered. | 
| Change Alert | If the alert conditions deviate from a prior value by a set percentage or value, an alert is triggered. | 
| Absence Alert | If the alert condition specifies a specific value or event must be present, the absence of that value or event will trigger an alert. | 
{% /table %}

## Interactive Demo

This interactive demo illustrates the configuration of an in-stream alert for a surge in financial data from a demo source. You will need to have pop-ups enabled for your browser or docs.mezmo.com to view the demo. You can also [view the demo without pop-ups](https://www.mezmo.com/demos/interactive-demo-in-stream-alerts) at mezmo.com.

{% html %}
<!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page -->
<button data-navattic-open="https://capture.navattic.com/clz0byns1000109ia0c8x8vib" data-navattic-title="In-Stream Alerts">
  Open the demo pop-up
</button>
{% /html %}