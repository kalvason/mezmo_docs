---
type: page
title: ElasticSearch
listed: true
slug: elasticsearch-destination
description: 
index_title: ElasticSearch
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/elasticsearch-pipeline-destination#description)

Typically you would use ElasticSearch to store and analyze large amounts of data which are of different structures and formats. An ElasticSearch cluster is composed of **Clusters**, **Indices**, **Nodes**, and **Shards** that help organize and manage how your data is stored. The data can then be efficiently and powerfully searched and analyzed.

ElasticSearch is usually used as a Pipeline destination when your log data needs to be indexed for searching. By setting up a Pipeline for your ElasticSearch data, you can use Pipeline Processors like [Dedupe](/telemetry-pipelines/dedupe-processor) and [Remove Fields](/telemetry-pipelines/drop-fields-processor) to clean data or drop it if it’s not valuable before sending it to ElasticSearch.

## [Configuration Options](https://docs.mezmo.com/docs/elasticsearch-pipeline-destination#configuration-options)

{% table widths="233" %}
| Option | Description | 
| ---- | ---- | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by ElasticSearch. | 
| Compression | Compression type to apply to your log data. | 
| Strategy | The authentication strategy of your ElasticSearch destination, with options for **Basic** and **AWS**. | 
| Endpoints | The full URL(s) of the ElasticSearch destination(s). | 
| Pipeline | The name of the ElasticSearch ingest pipeline to use. | 
| Custom Index | The index name or pattern of the ElasticSearch destination. | 
{% /table %}