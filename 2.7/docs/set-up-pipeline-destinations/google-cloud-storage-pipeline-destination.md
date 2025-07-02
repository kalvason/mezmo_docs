---
type: page
title: Google Cloud Storage
listed: true
slug: google-cloud-storage-pipeline-destination
description: 
index_title: Google Cloud Storage
hidden: 
keywords: 
tags: 
---

## Description

You can send your Mezmo Pipeline log data to Google Cloud Storage.

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Batch Timeout | The maximum amount of time for buffering events before being flushed to the destination. | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Google Cloud Storage. | 
| Strategy | The authentication strategy to use. | 
| Encoding | The type of encoding to use for serializing the data before sending it to storage. | 
| Bucket | The name of the Google Cloud Storage bucket to send your log data to. | 
| Compression | The type of compression to apply to the log data before sending it to storage. | 
| Bucket Prefix | The prefix to apply to the bucket name to set a directory for the stored data. | 
| API Key | The Google API Key to use for authentication. | 
{% /table %}