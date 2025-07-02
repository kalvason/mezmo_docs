---
type: page
title: AWS Kinesis Data Firehose
listed: true
slug: kinesis-firehose-destination
description: 
index_title: AWS Kinesis Data Firehose
hidden: 
keywords: 
tags: 
---

## Description

Publish logs to [AWS Kinesis Data Firehose](https://aws.amazon.com/kinesis/data-firehose) topics

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Access Key ID | AWS Access Key ID | 
| Secret Access Key | AWS Secret Access Key | 
| Encoding | The encoding to apply to the data. Either json or text | 
| Compression | Whether to compress the outgoing payload. Options: none or gzip | 
| Stream Name | The name of the Kinesis Firehose stream | 
| Region | The name of the AWS region that is targeted. | 
{% /table %}