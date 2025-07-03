---
type: page
title: Build and Deploy a Mezmo Edge Pipeline for Local Data
listed: false
slug: mezmo-edge
description: 
index_title: Build and Deploy a Mezmo Edge Pipeline for Local Data
hidden: 
keywords: 
tags: 
---

## Description

This Destination enables you to send log events to Google's Cloud Monitoring product. This Destination only supports log events. If you want to send metrics events, you should use the [Google Cloud Monitoring](/telemetry-pipelines/gcp-cloud-monitoring-destination) destination.

### Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Log ID | A concise reference used for the log stream name. | 
| Project ID | The [Project Id](https://support.google.com/googleapi/answer/7014113?hl=en) of your GCP Account. | 
| Resource Type | The resource type to which these events are related. | 
| Resource Labels | An array of key/val objects describing labels of the Monitoring resource. | 
| JSON Credentials | The Google Cloud [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating). | 
{% /table %}