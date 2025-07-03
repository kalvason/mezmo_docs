---
type: page
title: AWS SQS
listed: true
slug: sqs-source
description: 
index_title: AWS SQS
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/aws-s3-via-sqs-pipeline-source#description)

The AWS SQS Source enables you to stream log data from an SQS topic as a Pipeline source via Amazon's Simple Queue Service (SQS). 

## Configure SQS

1. Log in to the AWS console and navigate to **Simple Queue Service**.
2. On the Amazon SQS landing page, click **Create queue**.
3. For **Type**, make sure **Standard** is selected. 
4. Enter a **Name** for the service, for example `mezmo-pipeline`. 
5. Leave all the other settings at the default, and at the bottom of the page click **Create queue**. 
6. On the **Queue details** page, select the **Access policy** tab. 
7. Click **Edit** for the Access p**olicy**, and enter the JSON definition at the end of these instructions.  
8. In the JSON definition, enter these values, then click **Save**.
    1. For `Resource`, enter the value for `ARN` in the **Details** section for SQS. 
    2. For `aws:SourceARN`, navigate to your S3 bucket, open the **Properties** tab, and enter the value for `Amazon Resource Name (ARN).`
    3. For `aws:SourceAccount,` enter the value for your AWS user account. You can find your **Account ID** by selecting your account name in the upper-right corner of the AWS console.

### SQS Access Policy JSON Definition

{% code %}
{% tab language="json" %}
{
    "Version": "2012-10-17",
    "Id": "example-ID",
    "Statement": [
        {
            "Sid": "example-statement-ID",
            "Effect": "Allow",
            "Principal": {
                "Service": "s3.amazonaws.com"
            },
            "Action": [
                "SQS:SendMessage"
            ],
            "Resource": "SQS-queue-ARN",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:s3:*:*:awsexamplebucket1"
                },
                "StringEquals": {
                    "aws:SourceAccount": "bucket-owner-account-id"
                 }
            }
        }
    ]
}
{% /tab %}
{% /code %}

## AWS Access Key Required IAM Permissions

{% table %}
| Name | Purpose | 
| ---- | ---- | 
| [`sqs:ReceiveMessage`](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_ReceiveMessage.html) | Operation | 
| [`sqs:DeleteMessage`](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_DeleteMessage.html) | Operation | 
{% /table %}

## Mezmo Source [Configuration](https://docs.mezmo.com/docs/aws-s3-via-sqs-pipeline-source#configuration)

1. Select the Amazon SQS Source in your Mezmo Telemetry Pipeline and select **Edit config.** 
2. Navigate to your SQS queue and copy the **URL** in the **Details** section. 
3. In the Amazon SWS Source configuration, copy the URL into the **SQS Queue URL** field. 
4. Enter the information for your **AWS Authentication**, and the **Region** for your SQS Queue.
5. Select the Compression method to use for your SQS event notifications. The `Compression` setting of `auto` will attempt to use the `Content Encoding`, `Content-Type`, and `key` suffix to determine which encoding is in use. If the compression setting cannot be determined, it will default to `none`.

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/aws-s3-via-sqs-pipeline-source#mezmo-configuration-options)

{% table %}
| Option | Description | 
| ---- | ---- | 
| SQS Queue URL | The URL of an AWS SQS queue configured to receive S3 bucket notifications for the S3 buckets where your source data is stored. | 
| AWS Authentication - Access Key ID | The access key ID for your AWS account. | 
| AWS Authentication - Secret Access Key | The secret access key for your AWS account. | 
| Compression | The compression format for the S3 objects. | 
| Region | The name of the region for the S3 bucket. | 
{% /table %}

### Included Metadata

{% table %}
| Field | Format | Description | 
| ---- | ---- | ---- | 
| `file_name` | String | This is the name of the file being pulled | 
| `size` | Number | Number of bytes to be pulled | 
{% /table %}