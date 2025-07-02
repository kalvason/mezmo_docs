---
type: page
title: Google Cloud Monitoring
listed: true
slug: gcp-cloud-monitoring-destination
description: 
index_title: Google Cloud Monitoring
hidden: 
keywords: 
tags: 
---

## Description

This destination enables you to send metrics to Google's Cloud Monitoring product.  This Destination only supports metrics events.  If you want to send logs, you should use the [Google Cloud Operations](/2.8/telemetry-pipelines/gcp-cloud-operations-destination) Destination.

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Project ID | The [Project Id](https://support.google.com/googleapi/answer/7014113?hl=en) of your GCP Account. | 
| Resource Type | The [resource type](https://cloud.google.com/monitoring/api/resources) to which these events are related. | 
| Resource Labels | An array of key/value objects describing labels of the Monitoring resource. | 
| JSON Credentials | The Google Cloud [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating). | 
{% /table %}