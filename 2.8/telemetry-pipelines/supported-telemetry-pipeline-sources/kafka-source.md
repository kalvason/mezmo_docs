---
type: page
title: Kafka
listed: true
slug: kafka-source
description: 
index_title: Kafka
hidden: 
keywords: 
tags: 
---


## Description

This is a pull source. You can enable a source within Pipeline to collect events from Kafka compatible brokers.

## Configuration

You can configure the source as described in the table below.

### Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Title | Title of your source | 
| Description | Description of your source | 
| Brokers | A broker is an array of key/value pairs for each host and port of a Kafka broker | 
| Host | The host name of IP address of the broker | 
| Port | The port that the broker listens on | 
| Topics | List of Kafka topic names to read events from | 
| Consumer Group | The consumer group name to be used to consume events from Kafka | 
| TLS Enabled | On/off toggle for using TLS for outgoing messages | 
| SASL/SCRAM | On/off toggle for authentication | 
| Decoding | Choose from bytes or JSON | 
| SASL | Choose from plain, SCRAM-SHA-512, or SCRAM-SHA-256 | 
| Username | The SASL/SCRAM username | 
| Password | The SASL/SCRAM password | 
{% /table %}

{% /table %}