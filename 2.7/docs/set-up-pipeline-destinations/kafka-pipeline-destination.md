---
type: page
title: Kafka
listed: true
slug: kafka-pipeline-destination
description: 
index_title: Kafka
hidden: 
keywords: 
tags: 
---

## Description

You can send Mezmo Pipeline data to Kafka

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Kafka. | 
| Encoding | The type of encoding to use for your log data. | 
| Compression | The type of compression to use for your log data. | 
| Event Key Field | The log data field that Kafka will use as its event key. | 
| Broker IP and Port | The IP address and Port of the Kafka Broker you will use as your log data destination. | 
| Topic | The name of the topic to publish to. | 
| SASL/SCRAM Enabled | Enable SASL/SCRAM authentication for Kafka. | 
{% /table %}