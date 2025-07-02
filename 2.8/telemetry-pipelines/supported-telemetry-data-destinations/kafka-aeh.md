---
type: page
title: Azure Event Hub
listed: true
slug: kafka-aeh
description: 
index_title: Azure Event Hub
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/kafka-pipeline-destination#description)

You can send Mezmo Pipeline data to Azure Event Hub - utilizing their Kafka endpoint.

## [Configuration Options](https://docs.mezmo.com/docs/kafka-pipeline-destination#configuration-options)

One of the ways to send data to Azure Event Hubs is via their [Kafka endpoint](https://learn.microsoft.com/en-us/azure/event-hubs/azure-event-hubs-kafka-overview).  To configure your pipeline, please adjust your Kafka destination using the following options.

{% table widths="150,0" %}
| Option | Description | Value | 
| ---- | ---- | ---- | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by Kafka. |  | 
| Encoding | The type of encoding to use for your log data. |  | 
| Compression | The type of compression to use for your log data. |  | 
| Event Key Field | The log data field that Kafka will use as its event key. |  | 
| Broker IP and Port | This will be the kafka endpoint for your AEH namespace. | `<namespace name>.servicebus.windows.net:9093` | 
| Topic | The name of the topic to publish to. | Your event hub name | 
| Group ID | The consumer group identifier | If you are using default, please be sure to escape the dollar sign: `$$Default` | 
| Use TLS | Enable TLS connection to the endpoint | On | 
| TLS CA Certificate Chain | The CA certificate chain in PEM format | A valid CA chain like [this](https://curl.se/ca/cacert.pem). | 
| TLS Verify Certificate | Verify the TLS certificate | On | 
| SASL/SCRAM Enabled | Enable SASL/SCRAM authentication for Kafka. | On | 
| SASL | The SASL/SCRAM mechanism | `PLAIN` | 
| Username | The SASL/SCRAM Username | `$$ConnectionString` | 
| Password | The SASL/SCRAM Password | Set to the [AEH connection string](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string) | 
{% /table %}