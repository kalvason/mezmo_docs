---
type: page
title: AWS Cloudwatch Metrics
listed: true
slug: cloudwatch-metrics-destination
description: 
index_title: AWS Cloudwatch Metrics
hidden: 
keywords: 
tags: 
---

## Description

Send your metrics to[ AWS Cloudwatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)  for monitoring.

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Access Key ID | AWS Access Key ID | 
| Secret Access Key | AWS Secret Access Key | 
| Compression | Whether to compress the outgoing payload. Options: none or gzip | 
| Namespace | Name for the container that will isolate metrics from one another. | 
| Region | The name of the AWS region that is targeted. | 
{% /table %}

## Health Check

This sink is set up to automatically perform a health check on the AWS Cloudwatch Instance. In doing so, it will emit a `healthcheck` metric into your namespace.