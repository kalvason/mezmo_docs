---
type: page
title: Set In-Stream Alerts for Pipeline Nodes
listed: true
slug: set-in-stream-alerts
description: 
index_title: Set In-Stream Alerts for Pipeline Nodes
hidden: 
keywords: 
tags: 
---

You can set specific conditions to trigger an alert on any Source, or Processor in your Pipeline. Alerts are based on the aggregation of metrics or events within the data stream, and are triggered when when the aggregated data reaches meets specific conditions. 

## General Configuration

1. Log into [the Mezmo Web App](http://app.mezmo.com) and select the Pipeline where you want to set the alert, then click **Edit Pipeline**.
2. Select the Source, or Processor in your Pipeline where you want to set the alert, then click **Alerts**. 
3. Click **New Alert**.
4. Enter a **Name** and **Description** for the alert, then click **Next**. 

{% callout type="info" title="Alert Conditions Based on Egress Data" %}
When you configure alerts on a node, alert conditions are evaluated on the node's **egress data.**
{% /callout %}

## Evaluation Configuration

{% callout type="info" title="Selecting the Event Type" %}
In Step 2 of Evaluation Configuration, you need to select the `event type` for evaluation. This is to indicate if you are alerting on Metric events or Log events. Metric events have a standard schema and the aggregate processor can perform  standard operations by default. However,  Log events can have a varied schema, and you will  need to provide a custom aggregation script as described in Step 4.

For Metric event types, the available aggregation conditions are:

`Sum`, `Minimum`, `Maximum`, `Average`, `Set Intersection,` `Distribution Cocantenation`
{% /callout %}

Set the criteria for evaluation of the metric or event data. 

1. Select the **Alert Type**: **Threshold Alert**, **Change Alert**, or **Absence Alert**. 
2. Select the **Event Type**: **Metric**, **Event**. 
3. Select the field paths to use for aggregating and grouping events based on matching values. Default field paths are`.name`, `.namespace`, `.tags.`
4. Select the type of aggregating **Operation** to use: Sum, **Minimum**, **Maximum**, **Average**, **Set Intersection**, **Distribution Cocantenation**, or **Custom**. If you select **Custom**, enter the Script you want to use. Check out the topic [auto$](/telemetry-pipelines/js-script-processor) for more information about syntax for scripts.
5. Select the **Window Type**: **Tumbling** or **Sliding**. 
    1. **Tumbling** windows are a series of fixed-sized, non-overlapping and contiguous time intervals. For example, if you set it to a five-minute tumbling window, the elements with timestamp values [0:00:00-0:05:00) are in the first window. Elements with timestamp values [0:05:00-0:10:00) are in the second window.
    2. A **sliding** window has a fixed time length, and it moves forward or “slides” at a time interval smaller than the window’s length. For example, a sliding window can be five minutes long, and slide every one minute and capture five minutes of data. The length of the slide is not user-configurable by user, the system will automatically calculate an appropriate slide based on the window size.

6. Set the **Window Duration** for aggregation, in minutes.

## Alert Condition Configuration

Set the conditions that will trigger an alert based on the data evaluation.  All conditions are based on an IF statement. 

1. Enter the **Field** to use for the conditional statement. 
2. Select the **Operator** to use in the statement. 
3. Enter the **Value** to use. 
4. Click **Next**. 

As you enter the values, a conditional statement will be generated. For example:

{% code %}
{% tab language="bash" %}
if (.log_volume value_change_greater_or_equal 60)
{% /tab %}
{% /code %}

## Alert Event Structure

Internally, an alert instantiates an instance of the [auto$](/telemetry-pipelines/aggregate-processor) in order to track the configured Evaluation over time. The resulting alert event will consist of the event that triggered the alert, along with the `aggregate` results, which are stored in `metadata` . Any of this information can be extracted via [templates](/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values#templates) for use in the Alert Payload. 

This is an example of a Demo Logs Source that has an alert configured for it. Note the `aggregate` results inside of `metadata`, and the Demo Logs event that triggered the alert as the `message`.

{% code %}
{% tab language="javascript" %}
{
  "message": {
    "bytes": 8655,
    "datetime": "21/Aug/2024:17:35:34",
    "host": "100.49.129.84",
    "method": "HEAD",
    "protocol": "HTTP/1.1",
    "referer": "johns.com",
    "request": "/assets92ab70912ac7aca655b1016e84c1508",
    "status": 200,
    "user-identifier": "dockbradtke"
  },
  "metadata": {
    "aggregate": {
      "end_timestamp": 1724261783647,
      "event_count": 1,
      "start_timestamp": 1724261753647
    }
  }
}
{% /tab %}
{% /code %}

## Alert Payload Configuration

The Alert Payload enables you to customize the alert message based on the incoming alert event structure prior to sending it to an external service. Throttling is also used to control the frequency of alerts.

1. Select one of the available services and configure its options.
2. Configure the options for the selected service.
3. Set the **Throttling** options.
4. Click **Save**.

### Available Services

The available services to send alerts are Slack, PagerDuty, Webhook or Mezmo Log Analysis. These are the options for each service:

#### Slack

- URI - The full URI for the Slack API
- Message - A static or [templated](/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values#templates) string to be the Slack message

#### PagerDuty

- URI - The full URI for the [PagerDuty API](https://developer.pagerduty.com/docs/ZG9jOjExMDI5NTgx-send-an-alert-event)
- Summary - Details of the alert, as specified by their API docs. Supports [templating](/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values#templates).
- Severity - `INFO`, `WARNING`, `ERROR` or `CRITICAL`
- Source - The source of the alert. Supports templating.
- Routing Key - For PagerDuty authorization
- Event Action - `trigger`, `acknowledge` or `resolve`

#### Webhook

- URI - The full URI for the Webhook
- HTTP Method - `post`, `put`, `patch`, `delete`, `get`, `head`, `options` or `trace`
- Message - A static or [templated](/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values#templates) string as the webhook body. This can be a text string or serialized JSON. If the message can be parsed as JSON, it will be sent as such.
- HTTP Headers (optional)
- Authentication Options (optional)

#### Log Analysis

When using Mezmo Log Analysis, the Subject is the primary message in the payload. There will be additional properties appearing for `body and` `level` (Severity).

- Severity - The level of the log line: `INFO`, `WARNING`, `ERROR` or `CRITICAL`
- Subject - This text supports [templating](/telemetry-pipelines/syntax-for-editing-pipeline-component-configuration-values#templates), and will be easily seen in the Log Analysis UI.
- Body - Additional information to include in the payload. Supports templating.
- Mezmo Ingestion Key - the key to access your Log Analysis instance.

## View a Configured Alert

If a Source, Destination, or Processor has an alert configured, you will see an indicator on the node like this:

{% image url="https://uploads.developerhub.io/prod/2KW7/dbw00srjvvdcwlbkhnzrfz54yc9l4vykv74emopel8l2vou3399wiltfeiiojmkh.jpg" mode="responsive" height="198" width="257" %}
{% /image %}

You can see the alert configuration by clicking on the alert indicator.

## Interactive Demo

This demo illustrates the configuraiton of an in-stream alert for a Pipeline node. You will need to have pop-ups enabled for your browser or docs.mezmo.com to view the demo.  You can also v[iew the demo without a pop-up ](https://www.mezmo.com/demos/interactive-demo-in-stream-alerts)at mezmo.com.

{% html %}
<!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page -->
<button data-navattic-open="https://capture.navattic.com/clz0byns1000109ia0c8x8vib" data-navattic-title="In-Stream Alerts">
  View the demo in a pop-up
</button>
{% /html %}