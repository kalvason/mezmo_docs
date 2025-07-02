---
type: page
title: AWS Kinesis Streams
listed: true
slug: kinesis-streams-destination
description: 
index_title: AWS Kinesis Streams
hidden: 
keywords: 
tags: 
---


## Description

Publish logs to [AWS Kinesis Streams](https://aws.amazon.com/kinesis/data-streams) topics

Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Access Key ID | AWS Access Key ID | 
| Secret Access Key | AWS Secret Access Key | 
| Encoding | The encoding to apply to the data. Either json or text | 
| Compression | Whether to compress the outgoing payload. Options: none or gzip | 
| Stream Name | The name of the Kinesis Firehose stream | 
| Region | The name of the AWS region that is targeted. | 
| Partition Key Field | The field in the log whose value is used as Kinesis' partition key. | 
{% /table %}

{% /table %}