---
type: page
title: AWS SQS
listed: true
slug: sqs-destination
description: 
index_title: AWS SQS
hidden: 
keywords: 
tags: 
---


## Description

Publish observability events to [Simple Queue Service](https://aws.amazon.com/sqs/) topics

## Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Access Key ID | AWS Access Key ID | 
| Secret Access Key | AWS Secret Access Key | 
| Encoding | The encoding to apply to the data. Either json or text | 
| Region | The name of the AWS region that is targeted. | 
| SQS Queue URL | The URL of the SQS queue that the data is publishing to. | 
{% /table %}

{% /table %}