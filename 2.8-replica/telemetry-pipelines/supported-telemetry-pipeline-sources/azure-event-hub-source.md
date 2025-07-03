---
type: page
title: Azure Event Hub
listed: true
slug: azure-event-hub-source
description: 
index_title: Azure Event Hub
hidden: 
keywords: 
tags: 
---


## Description

This source enables you to ingest data from your Azure Event Hub instance into Mezmo Pipeline.

## Configuration

### Prerequisites

Azure Event Hubs (AEH) can be used to pull data into Mezmo Pipelines (Edge or Cloud) via the Kafka interface. **In order to use an AEH Source, you must make sure the Kafka interface surface is available.** For this reason your Event Hub namespace must be a Standard Tier or higher to be used as a Pipeline Source. See the[ Microsoft configuration instructions here for more details.](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create)

Once you have an appropriate namespace and have created or selected an Event Hub, you will need these  items:

1. A Shared Access Policy with Listen privileges on the Event Hub itself
    1. The namespace policy will not work

2. A connection string, either primary or secondary, from the Shared Access Policy on the Event Hub
3. A consumer group on the Event Hub **for each AEH Source** you intend to connect
    1. If you have a consumer group already, it may be in use. We recommend creating a new one for your pipeline in case the existing ones are in use.
    2. Note that a new consumer group will start from the beginning of the retention period for the Event Hub.

Your Event Hub must have active data flowing to check if the configuration is successful and verify data throughput.

### Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Title | Provide a title for your source | 
| Description | Provide a description for your source | 
| Connection String | The connection string as it appears in Event Hub | 
| Namespace | The Event Hub namespace | 
| Topics | The list of Event Hub names to read events from | 
| Consumer Group | The consumer group name that this consumer belongs to | 
| Decoding | Choose between bytes and json | 
{% /table %}

{% /table %}