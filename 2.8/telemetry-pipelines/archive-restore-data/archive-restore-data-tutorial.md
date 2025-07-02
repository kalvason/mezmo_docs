---
type: page
title: Tutorial: Create a Basic Data Archiving and Restoration Pipeline
listed: true
slug: archive-restore-data-tutorial
description: Learn to create a telemetry data pipelines for archiving and restoration using Mezmo's tools. This tutorial covers configuring archives to S3, restoring data to Mezmo Log Analysis, and managing pipelines with demo logs.
index_title: Tutorial: Create a Basic Data Archiving and Restoration Pipeline
hidden: 
keywords: 
tags: 
---

**Completion Time**: 10 Minutes

In this tutorial you'll learn how to create basic pipelines for telemetry data archiving and restoration using the [auto$](/telemetry-pipelines/mezmo-archive-destination),  the [auto$](/telemetry-pipelines/pipeline-data-restoration-source) Source, the  [Mezmo Log Analysis Destination](/telemetry-pipelines/mezmo-destination), and JSON [auto$](/telemetry-pipelines/demo-logs-source).

## Prerequisites

You should have an S3 bucket that you can use as the archiving destination. 

## Pipeline Architecture

These two Pipettes illustrate the basic configuration of a Pipeline to send telemetry data to an S3 bucket, and then restore that data and send it to Mezmo Log Analysis.

### Archive Pipeline

This Pipette sends [Demo Log](/telemetry-pipelines/demo-logs-source) HTTP JSON data directly to a [auto$](/telemetry-pipelines/mezmo-archive-destination) for archiving in an S3 bucket. 

For demonstration purposes this is a a two component Pipeline, but you would typically have processor groups [for converting events to metrics](/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics) or others to reduce log volume between the Source and the Archive Destination. 

{% image url="https://uploads.developerhub.io/prod/2KW7/swgjn63wykgguv2v8jmok30vkoywtarww2ztjemhifyx5a4zjafgxhjr9gfklu6z.png" caption="An example of sending data to an archiving destination." mode="responsive" height="468" width="1810" %}
{% /image %}

#### Demo Logs Source Configuration

{% table widths="" %}
| Configuration Option | Settting | 
| ---- | ---- | 
| **Interval** (the number of seconds to pause between sending logs) | `1` | 
| **Format** | `JSON HTTP` | 
{% /table %}

#### Mezmo Archive Destination Configuration

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Batch timeout (seconds)** | `300` | 
| **Archive Provider** | `S3` (note that you can also send archive logs to Azure) | 
| **Access Key ID** | Access key for the S3 bucket | 
| **Secret Access Key** | Secret access key for the S3 bucket | 
| **Bucket** | The name of the S3 bucket | 
| **Region** | The AWS region where the S3 bucket is located. | 
{% /table %}

### Restoration Pipeline

This Pipeline sends archived data from the [Pipeline Data Restoration Source](/telemetry-pipelines/pipeline-data-restoration-source), passes it through a [auto$](/telemetry-pipelines/filter-processor)  to drop data and a [auto$](/telemetry-pipelines/map-fields-processor) to make sure that the restored data conforms to the [required schema for the log analysis destination, ](/telemetry-pipelines/required-schema-for-mezmo-log-analysis-destination) and then finally sends it to Mezmo Log Analysis. 

Note that this Pipeline is not active after being saved and deployed. Data will only begin to stream when the Pipeline is activated during a **Restoration Task**, described in the next section. 

{% image url="https://uploads.developerhub.io/prod/2KW7/071o93zkkfz5xvg0ctrluuncgi9w9ekogttjxs1zqyh02qzh8zlracew8mnbhetf.png" mode="responsive" height="372" width="2004" %}
{% /image %}

#### Mezmo Pipeline Data Restoration Source Configuration

There is no configuration for the Source other than giving it a **Title**. This is how you will identify where to send the data for the restoration task. 

#### Filter Processor Configuration

This filter is set to only send a subset of the archived data to log analysis. 

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Action** | Drop events matching this criteria | 
| **Conditional Statement** | `if (message.status greater_or_equal 200 AND message.status less 300)` | 
{% /table %}

#### Map Fields Processor Configuration

This processor maps fields in the restored data to fields conform to the [schema required for Mezmo Log Analysis](/telemetry-pipelines/required-schema-for-mezmo-log-analysis-destination).

{% table widths="" %}
| Source Field | Target Field | 
| ---- | ---- | 
| `message.method` | `message.line` | 
| `message.referrer` | `.app` | 
{% /table %}

#### Mezmo Log Analysis Destination Configuration

{% callout type="info" title="Adding Tags for Search" %}
The tags you enter in the configuration options are intended to help you easily search for restored data in in the Log Viewer.
{% /callout %}

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Mezmo Host** | `logs.mezmo.com` | 
| **Ingestion Key** | The ingestion key for your Mezmo Log Analysis instance | 
| **Hostname** | `rehydrated-data` | 
| **Tags** (these will be attached to the restored data) | `{{metadata.query.tags}}` `restored` `restored- data` | 
| **Scheme** | `Message pass-through` | 
{% /table %}

## Create the Restoration Task

{% callout type="info" title="Admin Privileges Required" %}
You must have admin privileges within your Mezmo Organization to create and run a restoration task.
{% /callout %}

{% callout type="info" title="Match Restoration Task to Restoration Pipeline Account" %}
You should create the restoration task in the same account that is associated with the restoration pipeline.
{% /callout %}

1. In the Mezmo Web App, go to **Settings &gt; Archiving &gt; Pipeline Restoration**. 
2. Click **New Pipeline Restoration Task**. 
3. Enter a name for the restoration task. 
4. Enter the time period for the data you want to restore. 
5. Select the **Pipeline Archive** to restore data from. 
6. Select the Pipeline where you want to send the restored data. 
7. Click **Start**. You will see data begin to stream into the restoration pipeline, and then in your Mezmo Log Analysis viewer.