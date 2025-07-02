---
type: page
title: AWS S3 via SQS
listed: true
slug: s3-source
description: 
index_title: AWS S3 via SQS
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/aws-s3-via-sqs-pipeline-source#description)

The AWS S3 Source enables you to use log data stored in Amazon S3 as a Pipeline source via Amazon's Simple Queue Service (SQS). You would typically use Amazon S3 as a Pipeline source if you need to re-hydrate data for further analysis, due to an incident or for compliance. Once S3 data begins to flow through the Pipeline, you can specify data you don’t want to collect through a pipeline Processor to [parse](/telemetry-pipelines/parse-processor) specific fields, and [route](/telemetry-pipelines/route-processor) this parsed data to a metric analysis tool like Prometheus, or [Mezmo Log Analysis](/docs/about-mezmo-log-analysis). By re-hydrating, parsing, and routing only the Amazon S3 data you need to your analytical tools, you can minimize your costs to re-ingest your data.

## Configure SQS and S3

{% callout type="success" title="Set Up Your S3 Bucket First" %}
Because you will need some values from your S3 bucket configuration to complete the Access Policy configuration for SQS, you should set up your S3 bucket before you configure SQS. When you set up SQS, make sure that it is in the same region as your S3 bucket, or you will not be able to connect it to S3. You will only need to set up a basic S3 configuration, you will modify it to send data through SQS as part of these instructions.
{% /callout %}

### Configure SQS

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

### Configure S3

1. Navigate to your S3 bucket.
2. Select the **Properties** tab.
3. Scroll to the **Event notifications** section, and click **Create event notification**.
4. Enter an **Event name**, for example `mezmo-sqs-bucket-notify`.
5. Under **Event types**, for **Object creation**, select **Put**. This will send an event notification only when a new file or folder is added to the bucket. If you want to trigger notifications for other types of events, select those events.
6. Under **Destination**, choose `SQS queue`  and  then choose the queue you created above.
7. Click **Save changes**.

This completes the configuration of SQS and your S3 bucket. Now you can configure the Mezmo S3 source to receive S3 event notifications via SQS.

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

{% table widths="" %}

{% table %}
| Name | Purpose | 
| ---- | ---- | 
| [`s3:GetObject`](https://docs.aws.amazon.com/AmazonS3/latest/API/API_GetObject.html) | Operation | 
| [`sqs:ReceiveMessage`](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_ReceiveMessage.html) | Operation | 
| [`sqs:DeleteMessage`](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_DeleteMessage.html) | Operation | 
{% /table %}

{% /table %}

## Mezmo Source [Configuration](https://docs.mezmo.com/docs/aws-s3-via-sqs-pipeline-source#configuration)

1. Select the Amazon S3 Source in your Mezmo Telemetry Pipeline and select **Edit config.**
2. Navigate to your SQS queue and copy the **URL** in the **Details** section.
3. In the Amazon S3 Source configuration, copy the URL into the **SQS Queue URL** field.
4. Enter the information for your **AWS Authentication**, and the **Region** for your SQS Queue and S3 bucket.
5. Select the Compression method to use for your SQS event notificatinos. The `Compression` setting of `auto` will attempt to use the `Content Encoding`, `Content-Type`, and `key` suffix to determine which encoding is in use. If the compression setting cannot be determined, it will default to `none`.

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/aws-s3-via-sqs-pipeline-source#mezmo-configuration-options)

{% table widths="" %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| SQS Queue URL | The URL of an AWS SQS queue configured to receive S3 bucket notifications for the S3 buckets where your source data is stored. | 
| AWS Authentication - Access Key ID | The access key ID for your AWS account. | 
| AWS Authentication - Secret Access Key | The secret access key for your AWS account. | 
| Compression | The compression format for the S3 objects. | 
| Region | The name of the region for the S3 bucket. | 
{% /table %}

{% /table %}

### Included Metadata

{% table widths="" %}

{% table %}
| Field | Format | Description | 
| ---- | ---- | ---- | 
| `file_name` | String | This is the name of the file being pulled | 
| `size` | Number | Number of bytes to be pulled | 
| `bucket` | String | Where the file came from | 
{% /table %}

{% /table %}