---
type: page
title: Demo Pipeline Overview
listed: true
slug: demo-pipeline-guide8ke
description: 
index_title: Demo Pipeline Overview
hidden: 
keywords: 
tags: 
---


When you sign up for a free trial of Mezmo Telemetry Pipeline, a Demo Pipeline is automatically created for you to explore Pipeline features and functionality. This topic describes the architecture of the Demo Pipeline, along with highlights of its Sources, Processors, and Destinations.

## The Scenario

The Demo Pipeline is designed to illustrate a typical scenario, where there are multiple pipeline sources, a Route Processor that filters data based on conditional criteria, and additional processors for the filtered data that prepares it for routing to one destination for analysis, and another for archival storage. The specific scenario is a typical processing of JSON and Financial data to identify errors related to credit card transactions, which also requires encryption of credit card data before it can be sent to an analytical tool. In this guide, you'll see how to use the Route, Filter, and Encrypt Processors to accomplish this.

## Architecture Overview

To explore the Demo Pipeline in the Mezmo Web App:

1. Log in to [the Mezmo Web App](https://app.mezmo.com).
2. Click **Pipelines**.
3. Under **Deployed**, select **Demo Pipeline**.

If necessary, you can also click **Re-start Pipeline** to send the demo source data through the Pipaeline.

{% image url="https://uploads.developerhub.io/prod/2KW7/im66j3opusetyr53m3iuftld60g390jnzf0ftzsh8qjfbfchjurq1wbzs6m1xnwl.png" caption="The Demo Pipeline in the Mezmo Web App" mode="full" height="763" width="1538" %}
{% /image %}

### 1 Sources

The Demo Pipeline has two Sources, which are both versions of the [auto$](/telemetry-pipelines/demo-logs-source). You can use this Source to build your Pipelines using sample data before connecting them to live Production Sources, to make sure that your Processors are producing the results you want.


#### Financial Data and JSON

Use the [Pipeline Tap feature](/telemetry-pipelines/view-pipeline-data) to view the sample Financial  and JSON data. You can also download the sample data to view the full JSON, and build your own sample data.

{% image url="https://uploads.developerhub.io/prod/2KW7/bc8p4m7x3xf95iqfdfpj3l5mda275qrshabnmgrpqeggawbl30hwpfi02yubzl1o.png" caption="The Pipeline Tap view for the Financial Data Source" mode="600" height="648" width="985" %}
{% /image %}


#### JSON Data

{% image url="https://uploads.developerhub.io/prod/2KW7/elcklviivsaw1vgqdsm8ptf4krnjxtpys5d1hudx3lzas5aq6x2zkzrb3fa87eun.png" caption="The Pipeline Tap view for the JSON Data Source" mode="600" height="647" width="996" %}
{% /image %}

### 2 Route Processor

The [auto$](/telemetry-pipelines/route-processor) uses conditional statements to send data to other processors or destinations. In this case, there are four statements:

{% table %}

{% table %}
| Route Name | Purpose | Conditional Statement |  | Routed To | 
| ---- | ---- | ---- | ---- | ---- | 
| Purchase Transactions | Selects transaction events | `if (exists(.event) AND .event contains 'transaction')` |  | Allow "Card Denied" Filter | 
| Login/Logout Events | Selects login and logout events | `if (exists(.event) AND .event contains 'log')` |  | Drop Login/Logout Event Filter | 
| HTTP non-200s | Selects HTTP events that are not 200s (Success) | `if (exists(.status) AND .status greater 200)` |  | Long Term Analysis Destination | 
| Unmatched | Bucket for any data that is not selected by the other conditional statements | None |  | Archival Destination | 
{% /table %}

{% /table %}

You can test your Route Processor by using a [PIpeline Tap](/telemetry-pipelines/view-pipeline-data) to view the data flowing into it from the Sources, and inserting a tap for each route to make sure that data is passing through as expected.

### 3 and 4 Filter Processors

The Route Processor sends matched data to two [Filter Processors](/telemetry-pipelines/filter-processor).

{% table %}

{% table %}
| Filter Processor | Purpose | Conditional Statement | Routed To | 
| ---- | ---- | ---- | ---- | 
| Allow "Card Denied" | Filters the Purchase Transactions data to select those with a result of "Card Denied" | `if (.transaction.result_reason __contains 'card_denied')` | Encrypt Card Details Encrypt Field Processor | 
| Drop Login/Logout Events | Drops the Login/Logout Events matched by the Route Processor | `if (.access.action contains 'log')` | Long Term Analysis Destination | 
{% /table %}

{% /table %}

### 5 Encrypt Field Processor

For security compliance, credit card information should be encrypted before reaching the Long Term Analysis destination. With the [auto$](/telemetry-pipelines/encrypt-fields-processor), you can set encryption for a specific field, along with the encryption algorithm and key, and the Initialization Vector (IV) field.

{% table %}

{% table %}
| **Encrypted Field** | `.transaction.cc.cc_number` | 
| ---- | ---- | 
| **Encryption Algorithm** | `AES-256-CFB (key = 32 characters, iv=16 characters` | 
| **Encryption Key** | `keyenrcypt123456789keyenrcypt123` | 
| **Initialization Vector Field** | `.IVFIELD` | 
{% /table %}

{% /table %}

You can use the [auto$](/telemetry-pipelines/decrypt-fields-processor) with the same settings if you need to later decrypt the data.

### 6 Destinations

The routed and filtered data is sent to two versions of the [auto$](/telemetry-pipelines/blackhole-destination) destination, one representing Long Term Analysis, the other Archival Storage. As with the Demo Logs Pipeline Source, the Black Hole destination is useful for making sure your log data is processed as expected before connecting it to a Production Destination.