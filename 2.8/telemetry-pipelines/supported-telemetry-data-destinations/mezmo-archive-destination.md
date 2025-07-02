---
type: page
title: Mezmo Archive Destination
listed: true
slug: mezmo-archive-destination
description: 
index_title: Mezmo Archive Destination
hidden: 
keywords: 
tags: 
---

## Description

With this Destination, you can set up Archive locations for your telemetry data in S3 and Azure Cloud Storage, and then restore the data from those locations to a Pipeline using the [auto$](/telemetry-pipelines/archive-restore-data) feature. 

## Archiving Format and Frequency

If your data is being sent to the archive storage location  on  May 13, 2024, for example, the folder structure for your data files would follow this format: 

`bucket / year=2024 / month=05 / day=13`

By default, data is written to the Archive Destination every five minutes (though you can change this with the `Batch Timeout`value). or at 20k lines, or 10MB of data , whichever comes first.  Since these files are typically very small, there is an hourly  mechanism that will combine these smaller files into larger merged log files.

## Configuration

Configuration is similar to our S3 and Azure Blob Storage destinations, and appropriate rights must be set up for these destinations before configuring the Pipeline Destination.  Check out the topics for [auto$](/telemetry-pipelines/s3-destination) and [auto$](/telemetry-pipelines/azure-blob-storage-destination) for more details.

### Configuration Options

{% table widths="206" %}
| Option | Description | 
| ---- | ---- | 
| Batch Timeout | The maximum amount of time, in seconds, that events will be buffered before being flushed to the destination.\n\n\n\nDefault: 300s | 
| Archive Provider | The Cloud provider where you'd like to store your archives. | 
| **S3 Options** |  | 
| Access Key ID | The access key ID with permissions to your S3 bucket. | 
| Secret Access Key | The access key secret with permissions to your S3 bucket. | 
| Bucket | The bucket name.  \n\n\n\n Do not include a leading s3:// or a trailing / | 
| Region | Region in which your bucket is located. | 
| **Azure Blob Storage Options** |  | 
| Container Name | The name of the Azure Blob container. | 
| Connection String | The access key connection string with rights to this container. | 
{% /table %}

{% callout type="info" title="Info" %}
To aid with downstream processing of these archives, we will copy the event's `timestamp` field into the `message` field as `mezmo_timestamp` .
{% /callout %}