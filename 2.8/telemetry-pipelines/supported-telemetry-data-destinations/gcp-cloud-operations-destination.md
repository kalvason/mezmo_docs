---
type: page
title: Google Cloud Operations
listed: true
slug: gcp-cloud-operations-destination
description: 
index_title: Google Cloud Operations
hidden: 
keywords: 
tags: 
---

## Description

This destination enables you to send log events to Google's Cloud Monitoring product. This destination only supports log events. If you want to send metrics events, please use the [Google Cloud Monitoring](/telemetry-pipelines/gcp-cloud-monitoring-destination) destination.

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Log ID | A concise reference used for the log stream name. | 
| Project ID | The [Project Id](https://support.google.com/googleapi/answer/7014113?hl=en) of your GCP Account. | 
| Resource Type | The resource type related to these events. | 
| Resource Labels | An array of key/value objects describing labels of the Monitoring resource. | 
| JSON Credentials | The Google Cloud [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating). | 
{% /table %}