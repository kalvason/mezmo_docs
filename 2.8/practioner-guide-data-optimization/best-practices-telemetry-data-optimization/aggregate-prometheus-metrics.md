---
type: page
title: Aggregate Prometheus Metrics
listed: true
slug: aggregate-prometheus-metrics
description: 
index_title: Aggregate Prometheus Metrics
hidden: 
keywords: 
tags: 
---

Prometheus, with its multi-dimensional data model, is an ideal tool for monitoring system performance and detecting anomalies, but the data it produces must be optimized to reduce storage volume and produce meaningful insights. 

By using the  [auto$](/telemetry-pipelines/aggregate-processor-deprecate) to consolidate Prometheus metrics, you can significantly reduce the amount of data you are sending downstream to your observability tool. This processor aggregates multiple metric events into a single event based on a specified time interval, with options for **Sum**, **Minimum**, **Maximum**, and **Average** as the metric aggregation method, depending on the metric type, which is automatically detected.