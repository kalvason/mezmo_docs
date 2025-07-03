---
type: page
title: Google Cloud Storage
listed: true
slug: gcp-cloud-storage-destination
description: 
index_title: Google Cloud Storage
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/google-cloud-storage-pipeline-destination#description)

This destination enables you to send your Mezmo Pipeline log data to Google Cloud Storage.

## [Configuration Options](https://docs.mezmo.com/docs/google-cloud-storage-pipeline-destination#configuration-options)

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Batch Timeout | The maximum amount of time for buffering events before being flushed to the destination. | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Google Cloud Storage. | 
| Encoding | The type of encoding to use for serializing the data before sending it to storage. | 
| Bucket | The name of the Google Cloud Storage bucket to send your log data to. | 
| Compression | The type of compression to apply to the log data before sending it to storage. | 
| Bucket Prefix | The prefix to apply to the bucket name to set a directory for the stored data. | 
| JSON Credentials | The Google Cloud [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating) | 
{% /table %}

{% /table %}

{% callout type="info" title="Message Stored Only" %}
Please note that only the `message` portion of the [event envelope](/telemetry-pipelines/pipeline-event-data-model) will be stored.
{% /callout %}