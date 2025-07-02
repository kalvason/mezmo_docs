---
type: page
title: AWS S3 Storage
listed: true
slug: s3-destination
description: 
index_title: AWS S3 Storage
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/amazon-s3-storage-pipeline-destination#description)

Typically you would send data to an AWS S3 bucket for long-term storage, or to send a subset of the data to a database. By sending your data through a Mezmo Pipeline before sending it to S3, you can [encrypt](/telemetry-pipelines/encrypt-fields-processor) sensitive data, [remove fields](/telemetry-pipelines/drop-fields-processor) you don't need to store, and [compact](/telemetry-pipelines/compact-fields-processor) values to make sure the data you’re storing is complete for easy retrieval and rehydration in case you need it later.

## [Configuration Options](https://docs.mezmo.com/docs/amazon-s3-storage-pipeline-destination#configuration-options)

{% callout type="info" title="Required Permissions in IAM" %}
When setting up your Access Key in IAM, ensure you have the following permissions on your bucket:

`s3:ListBucket`

`s3:PutObject`
{% /callout %}

{% table %}

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

{% /table %}

{% callout type="info" title="Message Only Stored" %}
Please note that only the `message` portion of the [event envelope](/telemetry-pipelines/pipeline-event-data-model) will be stored.
{% /callout %}