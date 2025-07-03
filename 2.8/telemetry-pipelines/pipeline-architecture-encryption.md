---
type: page
title: Pipeline Example: Drop, Encrypt, and Route Data to  Storage
listed: false
slug: pipeline-architecture-encryption
description: 
index_title: Pipeline Example: Drop, Encrypt, and Route Data to  Storage
hidden: 
keywords: 
tags: 
---

Based on [the Mezmo Workshop of the same name](https://logdna.github.io/mezmo-workshops/transaction-to-s3/), this topic and video illustrates the architecture of a Pipeline with processors for identifying data that contains sensitive information like credit card numbers and expiration dates, and then routing and encrypting that data for storage in an Amazon S3 bucket.

## [Source](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#source)

### Demo Logs

For this example, the Source is our [Pipeline Demo Logs](https://docs.mezmo.com/telemetry-pipelines/demo-logs-source). Name it **Edge Devices**, choose format **Financial** from the drop down and click **Save**.

## [Processors](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#processors)

### [Remove Fields](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#remove-fields)

The [auto$](/telemetry-pipelines/drop-fields-processor), named **Drop Buffer** in this map, is set to remove all fields named `.buffer`at the beginning of the pipeline, since these fields don't need encryption processing.

### [Route](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#route)

The [auto$](/telemetry-pipelines/route-processor), named **Route Transaction** in this map, uses conditional logic to identify data that could contain transaction information, and then sends that through the **Encryption** processors before being stored in Amazon S3. Data that doesn't match the criteria for transaction information is routed directly to Mezmo Log Analysis.

#### Settings

{% code %}
{% tab language="none" title="" %}
IF transaction.result equal success
AND transaction.total_price is_greater_or_equal_to 0 

Transaction Failure

IF transaction.result equal fail
AND transaction.total_price not 0
{% /tab %}
{% /code %}

The resulting conditional statements in your Route Processor should look like this:

{% table %}
| Route Name | Conditional Statemenet | Destination | 
| ---- | ---- | ---- | 
| Transaction Success | `if (.transaction.result equal 'success' AND .transaction.total`_`price greater`_`or_equal 0)` | Encrypt | 
| Transaction Failure | `if (.transaction.result equal 'fail' AND .transaction.total_price not_equal '0 ')` | None | 
{% /table %}

Each of these matching criteria are displayed within the **Route Processor** node in the map, along with the **Unmatched** condition. Each of these conditions are then connected to the the other Pipeline components, with the matching data routed to the Encryption processors, and the unmatched data routed to Mezmo Log Analysis.

### [Encryption](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#encryption)

The matching data is sent through five [Encrypt Field Processors](/telemetry-pipelines/encrypt-fields-processor), which encrypt the credit card number, the expiration date, the CVV number, the name on the credit card, and the associated Zip Code.

#### Settings

Each Encrypt Processor uses the same **Encryption Algorithm**, but identifies a different field for encryption, along with a unique encryption key for that field.

{% table %}
| Processor | Encrypted Field | 
| ---- | ---- | 
| Encrypt CC Number | `transaction.cc.cc_number` | 
| Encrypt CC Ex. # | `transaction.cc.cc_expiration` | 
| Encrypt CVV for CC | `transaction.cc.cc_cvv` | 
| Encrypt CC Name | `transaction.cc.cc_number` | 
| Encrypt CC Zip Code | `transaction.cc.cc`_`zip`_`code` | 
{% /table %}

If you need to decrypt data that you've put into storage, you can use the [auto$](/telemetry-pipelines/decrypt-fields-processor) in a Processor chain that applies the same Encryption Key to the same fields that you set up in your encryption pipeline.

## [Destinations](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#destinations)

### [Amazon S3](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#amazon-s3)

Data that has been passed through the Encryption processors is finally sent to a pre-configured Amazon S3 bucket as its destination.

**Settings**

The configuration settings for the S3 bucket destination include:

{% table %}
| Configuration Option | Description | 
| ---- | ---- | 
| AWS Access Key | The access key ID for your Amazon S3 account. | 
| AWS Secret Access Key | The access key secret for your Amazon S3 account. | 
| S3 Bucket | The Amazon S3 bucket to use as your storage destination. | 
{% /table %}

You can find a complete list of configuration settings in the [auto$](/telemetry-pipelines/s3-destination) topic.

### [Mezmo Log Analysis](https://docs.mezmo.com/docs/pipeline-architecture--encrypt--drop--and-route-data-to-amazon-s#mezmo-log-analysis)

Data that doesn't meet the matching criteria for transaction data is sent directly to Mezmo Log Analysis.

#### Settings

The configuration settings for the Mezmo Log Analysis destination include:

{% table %}
| Configuration Option | Description | 
| ---- | ---- | 
| Mezmo Host | The URI for your Mezmo Log Analysis host environment. This option is auto-configured based on your Mezmo account. | 
| Hostname | The tag to use to identify the origin of your logs | 
| Ingestion Key | Your Mezmo ingestion key. You can find this by logging into the Mezmo Web App and navigating to **Settings &gt; Organization &gt; API Key**. | 
{% /table %}

## Video Overview

{% video videoId="821469112" provider="vimeo" %}
{% /video %}