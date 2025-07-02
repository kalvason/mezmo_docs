---
type: page
title: Azure Blob Storage
listed: true
slug: azure-blob-storage-destination
description: 
index_title: Azure Blob Storage
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/azure-cloud-storage-pipeline-destination#description)

You can send your Mezmo Pipeline log data to Azure for storage.

## [Configuration Options](https://docs.mezmo.com/docs/azure-cloud-storage-pipeline-destination#configuration-options)

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Batch Timeout | The amount of time, in seconds, to buffer your log data before sending it to Azure. | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Azure. | 
| Encoding | The type of encoding to use for your log data. | 
| Compression | The type of compression to apply to your log data as it is sent to the S3 bucket. | 
| Container Name | The name of the Azure Blob container to use for your log data. | 
| Connection String | The connection string, including Access Key, to use for connecting to the container.\n\n\n\n\n\n\n\nYou may also use a [Shared Access Signature](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview) string if you do not wish to use an Access Key. The format must match the connection string standard:\n\n\n\n\n`BlobEndpoint=`[`https://<MYSTORAGEACCOUNT>.blob.core.windows.net`](https://dominicmcallistermezmo.blob.core.windows.net/)`;SharedAccessSignature=<SIGNATURE>` | 
| Storage Account | The name of the Azure Blob Storage account. | 
| Prefix | A prefix to apply to all object key names. | 
{% /table %}

{% /table %}

{% callout type="info" title="Message Stored Only" %}
Please note that only the `message` portion of the [event envelope](/telemetry-pipelines/pipeline-event-data-model) will be stored.
{% /callout %}