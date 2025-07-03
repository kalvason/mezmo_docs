---
type: page
title: Archive and Restore Telemetry Data
listed: true
slug: archive-restore-data
description: 
index_title: Archive and Restore Telemetry Data
hidden: 
keywords: 
tags: 
---

Mezmo offers several Pipeline components and features to help you archive and restore telemetry data for later analysis.

## Archive Destination

The  [auto$](/telemetry-pipelines/mezmo-archive-destination) enables you to store your events in either S3 or Azure.  This Destination is designed to be compatible with the [auto$](/telemetry-pipelines/pipeline-data-restoration-source) Source, but you can use it with other tools that can interface with Azure and S3.

## Pipeline Data Restoration Source

The Mezmo [Pipeline Data Restoration Source](/telemetry-pipelines/pipeline-data-restoration-source)  enables you to send data from Mezmo's Archive Destination into a Pipeline.  This source expects your data to either be regular text log lines or NDJSON.  There is no specific schema expected of NDJSON.

## Restore Telemetry Data to a Pipeline or Log Analysis

1. In the Mezmo Web app, go to **Archiving &gt; Pipeline Restoration**.
2. Enter a **Name** for the Restoration Task. 
3. Enter the **Time range** for the data you want to restore. 
4. Select the **Archive** you want to restore the data from. 
5. Select the **Destination** where you want to restore the data. 

### Archive Options

{% table widths="" %}
| Option | Description | 
| ---- | ---- | 
| **Pipeline Archive** | When you select this option, the menu will populate with a list of the [auto$](/telemetry-pipelines/mezmo-archive-destination)s in any of your Pipelines, and connection will be based on the configuration of the selected Destination. | 
| **Log Analysis Archive** | When you select this option, the task will connect to the  [Archives you have set up in Mezmo Log Analysis](/docs/archiving). | 
{% /table %}

### Destination Options

Restoration data sent to log analysis must conform to the[ required schema](https://docs.mezmo.com/telemetry-pipelines/required-schema-for-mezmo-log-analysis-destination). 

{% table widths="" %}
| Option | Description | 
| ---- | ---- | 
| **Send to Pipeline** | When you select this option, the menu will populate with a list of the [auto$](/telemetry-pipelines/pipeline-data-restoration-source) Sources in your Pipelines. | 
| **Send to Log Analysis** | When you select this option, the task will create a [log restoration task](/docs/data-restoration) and restore logs to a [Mezmo Log Analysis Destination](/telemetry-pipelines/mezmo-destination). | 
{% /table %}

####