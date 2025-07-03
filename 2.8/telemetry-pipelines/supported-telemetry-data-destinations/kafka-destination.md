---
type: page
title: Kafka
listed: true
slug: kafka-destination
description: 
index_title: Kafka
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/kafka-pipeline-destination#description)

You can send Mezmo Pipeline data to Kafka.

## [Configuration Options](https://docs.mezmo.com/docs/kafka-pipeline-destination#configuration-options)

{% table widths="150" %}
| Option | Description | 
| ---- | ---- | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Kafka. | 
| Encoding | The type of encoding to use for your log data. | 
| Compression | The type of compression to use for your log data. | 
| Event Key Field | The log data field that Kafka will use as its event key. | 
| Broker IP and Port | This will be the kafka endpoint for your AEH namespace. | 
| Topic | The name of the topic to publish to. | 
| Group ID | The consumer group identifier | 
| Use TLS | Enable TLS connection to the endpoint | 
| TLS CA Certificate Chain | The CA certificate chain in PEM format | 
| TLS Verify Certificate | Verify the TLS certificate | 
| SASL/SCRAM Enabled | Enable SASL/SCRAM authentication for Kafka. | 
| SASL | The SASL/SCRAM mechanism | 
| Username | The SASL/SCRAM Username | 
| Password | The SASL/SCRAM Password | 
{% /table %}