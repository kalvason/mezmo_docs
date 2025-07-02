---
type: page
title: Logstash
listed: true
slug: logstash-pipeline-source
description: 
index_title: Logstash
hidden: 
keywords: 
tags: 
---

## Description

You can send data from your Logstash instance to Mezmo Pipelines. 

## Configuration

Select the data format to ingest based on how you configure the Logstash output plugin. We recommend using the [HTTP output plugin documented here](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-http.html).

Form encoding is not supported at this time, so use string or json methods for output formatting.

### Mezmo Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Data Format | The format of the log data. | 
{% /table %}