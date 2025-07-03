---
type: page
title: Condense Kafka Logs into Metrics
listed: true
slug: condense-kafka-logs-into-metrics
description: 
index_title: Condense Kafka Logs into Metrics
hidden: 
keywords: 
tags: 
---


Kafka, an event streaming platform, generates an enormous amount of data from various types of transactions. While this full coverage maintains the fidelity of the original data, it also generates a large volume of data for storage and processing, and sifting through this data to generate meaningful information can be a tedious process. With the [auto$](/telemetry-pipelines/event-to-metric-processor) you can transform repetitive Kafka log events into summary metrics that can then be passed to observability tools for further analysis. This is especially useful in situations where there is high tag cardinality for events, producing a streamlined summary of information. It can output metrics as counter, sum, or gauge, and can provide incremental metrics for a dynamic view of data.