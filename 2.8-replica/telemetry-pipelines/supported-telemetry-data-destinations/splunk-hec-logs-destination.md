---
type: page
title: Splunk HTTP Event Collector
listed: true
slug: splunk-hec-logs-destination
description: 
index_title: Splunk HTTP Event Collector
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/splunk-http-event-collector-pipeline-destination#description)

You can send Mezmo Pipeline log data to Splunk.

## [Configuration Options](https://docs.mezmo.com/docs/splunk-http-event-collector-pipeline-destination#configuration-options)

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Splunk. | 
| Encoding | The encoding to apply to your log data. | 
| Compression | The compression to apply to your log data | 
| Endpoint | The base URL for your Splunk instance. The Collector path will be inferred from this base URL. | 
| Token | Token to use to authenticate your connection to Splunk | 
| Verify TLS Certificate | Enable to verify that the Splunk instance has a valid TLS certificate. This will not establish a secure connection, but can be useful for testing the Splunk destination. | 
| Host Field | The log data field to use for sending the hostname to Splunk. | 
| Indexed Fields | The field or fields for Splunk to extract into its index. | 
{% /table %}

{% /table %}