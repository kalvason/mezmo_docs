---
type: page
title: Tutorial: Route Data
listed: true
slug: pipeline-module--route
description: 
index_title: Tutorial: Route Data
hidden: 
keywords: 
tags: 
---

In more complex architectures, you will often have several Sources feeding into the same Pipeline, with the data for each needing different types of processing before being sent to multiple destinations. A key component of these Pipelines is a Route Processor, which uses conditional statements to match data and send it along its particular processing route. 

This topic describes a typical use of a Route Processor, with examples of the Processor configurations. 

## Interactive Demo

You can see how data is processed and routed through a Pipeline with this interactive demo. To view the demo you will need to have pop-ups enabled for your browser or docs.mezmo.com. You can also [view this demo without a pop-up](https://www.mezmo.com/demos/interactive-demo-route) at mezmo.com. 

{% html %}
<!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page -->
<button data-navattic-open="https://capture.navattic.com/clxcejvho00010al9cf7q9b1y" data-navattic-title="Route Processor">
  View the demo in a pop-up
</button>
{% /html %}

## Overview

This schematic illustrates the configuration of a Routing group, which includes a Script Execution Processor to format raw strings to JSON, that routes different data types from several sources through specialized processing chains to several destinations. 

{% image url="https://uploads.developerhub.io/prod/2KW7/3nxo3tdofxzio0vl8y9wi9pp9ix6nnd83b5iz3mr6xjcwinx11san4fi9e5u6ju8.png" mode="responsive" height="446" width="1496" %}
{% /image %}

## 1 - Sources

The Sources represent three different types of data flowing through the Pipeline that need to be routed to separate processing chains:

1. **Financial Data** that needs to have Personally Identifying Information encrypted before being sent to storage and the observability tool. 
2. **JSON Data** that needs to have Status - 200 **events** routed and dropped.
3. **Apache Errors** that need to be converted to JSON format and all info messages dropped. 

{% callout type="info" title="Try It with Demo Sources" %}
1. Log into the Mezmo App, and in the **Pipelines** section, click **New Pipeline**.
2. Add three  **Demo Logs** Sources, and for **Format**, select 1) **Financial Data** 2) **JSON** 3) **Apache Errors**. 
3. Add three  **Blackhole** Destinations to your Pipeline to represent 1) **Drop** 2) **Storage** 3) **Observability Tool**. 
4. Add the Processors and their configurations as shown in this example.
5. To view the data transformations through the Processors, **Deploy** the Pipeline, and then click the **Tap** for the Source and each Processor to see the data as it egresses from each node. 

If you don't yet have a Mezmo account, you can [sign up for a 30 Day Free Trial](https://www.mezmo.com/sign-up-pipeline-today) to try us out!
{% /callout %}

## 2 - Script Execution Processor

The [auto$](/telemetry-pipelines/js-script-processor) is configured to convert the Apache errors from raw strings to JSON format. 

{% code %}
{% tab language="bash" title="JSON Conversion Script" %}
function junk(message) {
  var new_message = {}
  new_message.message = message
  return new_message
}
{% /tab %}
{% /code %}

## 3 - Route Processor

The [auto$](/telemetry-pipelines/route-processor) uses three conditional statements to identify and route specific components of all three data types:

#### Apache Info Messages

{% code %}
{% tab language="javascript" title="Info Conditional Statement" %}
if (exists(.message) AND .message contains 'INFO')
{% /tab %}
{% /code %}

Because both the JSON and Apache errors data contain .message fields, this statement uses AND to make sure that that .messages that don't contain the INFO event won't generate a "field not found" error.  All messages meeting this criteria are sent to the Drop Destination. 

#### Status 200 Events

{% code %}
{% tab language="javascript" title="Status - 200 Events Conditional Statement" %}
if (exists(.status) AND .status equal 200)
{% /tab %}
{% /code %}

All events that meet these criteria are sent to the Drop Destination. 

#### Transaction Events

{% code %}
{% tab language="bash" title="Transaction Conditional Statement" %}
if (exists(.event) AND .event equal 'transaction')
{% /tab %}
{% /code %}

All events that meet these criteria are send to the Encrypt Processor. 

## 4 - Encrypt Processor

Because transaction events contain Personally Identifying Information (PII), such as credit card numbers, this information needs to be encrypted before being sent to storage and observability tools. For more information, check out the topic [auto$](/practioner-guide-data-optimization/pipeline-module--security-and-compliance).

**Encrypt Processor Configuration**

{% table widths="" %}
| Configuration Field | Details | 
| ---- | ---- | 
| Field | .transaction.cc.cc_number | 
| Encryption algorithm | AES-256-CFB (key=32 characters, iv-16 characters) | 
| Encryption key | zipadeedoodah012zipadeedoodah013 | 
| Intialization vector (IV) field | .creditcardnumber | 
{% /table %}

## 5 - Destinations

The routed data is sent to three destination, represented in this schematic by the [Black Hole Destination](/telemetry-pipelines/blackhole-destination):

1. **Drop**, where the unnecessary INFO and Status - 200 mesages are sent. 
2. **Storage**, where all unmatched data and encrypted PII data is sent. 
3. **Observability Tool,** where all unmatched data and encrypted PII data is sent.

The [auto$](/telemetry-pipelines/blackhole-destination) Destination drops all data sent to it. This makes it useful for testing your Processor chain to make sure you are getting the expected results before sending them on to a production Destination. Mezmo supports a wide variety of popular Destinations including [auto$](/telemetry-pipelines/mezmo-destination), [auto$](/telemetry-pipelines/datadog-metrics-destination), and [auto$](/telemetry-pipelines/prometheus-remote-write-destination).