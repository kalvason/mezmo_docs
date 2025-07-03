---
type: page
title: AWS Cloudwatch Logs
listed: true
slug: cloudwatch-logs-destination
description: 
index_title: AWS Cloudwatch Logs
hidden: 
keywords: 
tags: 
---


## Description

Send your logs to [AWS Cloudwatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html) for monitoring.

## Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Access Key ID | AWS Access Key ID | 
| Secret Access Key | AWS Secret Access Key | 
| Encoding | The encoding to apply to the data. Either text or json | 
| Compression | Whether to compress the outgoing payload. Options: none or gzip | 
| Group Name | The name of the log group for the targeted log stream. | 
| Region | The name of the AWS region that is targeted. | 
| Stream Name | The name of the targeted log stream. | 
{% /table %}

{% /table %}