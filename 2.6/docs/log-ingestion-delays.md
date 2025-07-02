---
type: page
title: Log Ingestion Delays
listed: true
slug: log-ingestion-delays
description: 
index_title: Log Ingestion Delays
hidden: 
keywords: 
tags: 
---




Periodically there will be delays in processing new log data due to the volume of incoming logs. This topic describes the two types of delays you may experience during log ingestion: **Live Tail Latency** and Indexing **Latency** .

## Live Tail Latency

Mezmo aims for an operational standard of 1s for Live Tail latency. The typical average for Live Tail latency is approximately 10s. You can view the current latency at [https://status.Mezmo.com](https://status.Mezmo.com).

## Indexing Latency

Indexing refers to the time between when a log line is ingested, and when it's available for search. By default, the Mezmo indexing process updates every 30s. As soon as a line is available in Live Tail, it should be indexed by Mezmo within 30s.





