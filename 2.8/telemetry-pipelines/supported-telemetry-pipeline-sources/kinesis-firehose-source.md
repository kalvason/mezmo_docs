---
type: page
title: AWS Kinesis Firehose
listed: true
slug: kinesis-firehose-source
description: 
index_title: AWS Kinesis Firehose
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/aws-kinesis-firehose-pipeline-source#description)

The AWS Kinesis Firehose Pipeline Source enables streaming of near realtime data to your Mezmo Pipeline.

An example edit. 

## [Configuration](https://docs.mezmo.com/docs/aws-kinesis-firehose-pipeline-source#configuration)

For convenience, each AWS Kinesis Firehose `records` item will be unrolled into its own event within this Oipeline. If you specify that data as being JSON, it will be automatically parsed for you.

For Kinesis Data Firehose to successfully deliver data to custom HTTP endpoints, these endpoints must accept requests and send responses using certain Kinesis Data Firehose request and response formats. These formats are documented in the [AWS Kinesis Firehose Developer Guide](https://docs.aws.amazon.com/firehose/latest/dev/httpdeliveryrequestresponse.html). To use Firehose as a source for Mezmo Pipelines, you must add your API key into the configuration of the Firehose Delivery Stream.

1. In your AWS Kinesis Firehose account settings, under the **HTTP endpoint URL**, enter the endpoint listed in your Kinesis Firehose source. 
2. Under the **Access key -** _**optional**_ section, choose **Update current access key** and enter the API key.
3. Click **Save Changes.**

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/aws-kinesis-firehose-pipeline-source#mezmo-configuration-options)

{% table widths="" %}
| Option | Description | 
| ---- | ---- | 
| Data Format | The format to use for the log data. | 
{% /table %}