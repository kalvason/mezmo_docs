---
type: page
title: AWS S3 via SQS
listed: true
slug: aws-s3-via-sqs-pipeline-source
description: 
index_title: AWS S3 via SQS
hidden: 
keywords: 
tags: 
---

## Description

The AWS S3 Source enables you to use log data stored in Amazon S3 as a Pipeline source via Amazon's Simple Queue Service (SQS). You would typically use Amazon S3 as a Pipeline source if you need to re-hydrate data for further analysis, due to an incident or for compliance. Once S3 data begins to flow through the Pipeline, you can specify data you don’t want to collect through a pipeline Processor to [parse](/docs/parse-pipeline-processor) specific fields, and [route](/docs/route-pipeline-processor) this parsed data to a metric analysis tool like Prometheus, or [auto$](/docs/mezmo-log-analysis-pipeline-destination). By re-hydrating, parsing, and routing only the Amazon S3 data you need to your analytical tools, you can minimize your costs to re-ingest your data.

## Configuration

The **Compression** setting of **auto** will attempt to use the **Content Encoding**, **Content-Type**, and **key** suffix to determine which encoding is in use. If the compression setting cannot be determined, it setting will default to `none`. 

### Mezmo Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| SQS Queue URL | The URL of an AWS SQS queue configured to receive S3 bucket notifications for the S3 buckets where your source data is stored. | 
| AWS Authentication - Access Key ID | The access key ID for your AWS account. | 
| AWS Authentication - Secret Access Key | The secret access key for your AWS account. | 
| Compression | The compression format for the S3 objects. | 
| Region | The name of the region for the S3 bucket. | 
{% /table %}