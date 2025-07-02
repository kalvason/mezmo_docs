---
type: page
title: Azure Blob Storage
listed: true
slug: azure-cloud-storage-pipeline-destination
description: 
index_title: Azure Blob Storage
hidden: 
keywords: 
tags: 
---

## Description

You can send your Mezmo Pipeline log data to Azure for storage.

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Batch Timeout | The amount of time, in seconds, to buffer your log data before sending it to Azure. | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Azure. | 
| Encoding | The type of encoding to use for your log data. | 
| Compression | The type of compression to apply to your log data as it is sent to the S3 bucket. | 
| Container Name | The name of the Azure Blob container to use for your log data. | 
| Connection String | The connection string, including Access Key, to use for connecting to the container. | 
| Storage Account | The name of the Azure Blob Storage account. | 
| Prefix | A prefix to apply to all object key names. | 
{% /table %}