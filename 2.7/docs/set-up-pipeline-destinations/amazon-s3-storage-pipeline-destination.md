---
type: page
title: Amazon S3 Storage
listed: true
slug: amazon-s3-storage-pipeline-destination
description: 
index_title: Amazon S3 Storage
hidden: 
keywords: 
tags: 
---

## Description

Typically you would send data to an AWS S3 bucket for long-term storage, or to send a subset of the data to a database. By sending your data through a Mezmo Pipeline before sending it to S3, you can [encrypt](/docs/encrypt-field-pipeline-processor) sensitive data, [remove fields ](/docs/remove-fields-pipeline-processor)you don't need to store, and [compact](/docs/compact-fields-pipeline-processor) values to make sure the data you’re storing is complete for easy retrieval and rehydration in case you need it later. The topic [auto$](/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s) provides an example of how you can set up a Pipeline to process sensitive data before sending it to S3 for storage. 

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Batch Timeout | The maximum amount of time for buffering events before being flushed to the destination. | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by S3. | 
| AWS Access Key ID | The access key ID for your Amazon S3 account. | 
| AWS Secret Access Key | The access key secret for your Amazon S3 account | 
| S3 Bucket | The Amazon S3 bucket to use as your storage destination. | 
| Prefix | A prefix to apply to all object key names. | 
| Tags | Any tags to apply to your log data. | 
| Encoding | The type of encoding to use for your log data. | 
| Compression | The type of compression to apply to your log data as it is sent to the S3 bucket. | 
| Region | The AWS region for your S3 bucket. | 
{% /table %}