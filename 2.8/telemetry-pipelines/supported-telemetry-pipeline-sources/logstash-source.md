---
type: page
title: LogStash
listed: true
slug: logstash-source
description: 
index_title: LogStash
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/logstash-pipeline-source#description)

You can send data from your Logstash instance to Mezmo Pipelines.

## [Configuration](https://docs.mezmo.com/docs/logstash-pipeline-source#configuration)

Select the data format to ingest based on how you configure the Logstash output plugin. We recommend using the [HTTP output plugin documented here](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-http.html).

Form encoding is not supported at this time, so use string or json methods for output formatting.

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/logstash-pipeline-source#mezmo-configuration-options)

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Data Format | The format of the log data. | 
{% /table %}

{% /table %}