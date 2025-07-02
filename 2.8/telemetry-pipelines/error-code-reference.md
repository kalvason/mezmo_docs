---
type: page
title: Error Code Reference
listed: true
slug: error-code-reference
description: 
index_title: Error Code Reference
hidden: 
keywords: 
tags: 
---


This topic describes the Error Codes and their associated messages for the Mezmo Telemetry Pipeline.

{% table widths="138,304" %}

{% table %}
| **Processor Errors** |  |  | 
| ---- | ---- | ---- | 
| **Component** | **Error Code** | **Error Message** | 
| General | `E_NOT_FOUND` | The field specified was not found in the incoming event(s) | 
| Compact | `E_COMPACT_BAD_TYPE` | The field to compact contained a value that was not an object nor array as required | 
| Decrypt | `E_DECRYPT_BAD_IV` | The initialization vector value was not a string as required | 
| Decrypt | `E_DECRYPT_BAD_TYPE` | The field to decrypt was not a string value as required | 
| Decrypt | `E_DECRYPT_FIELD_DECODE` | The field value was not a base64 encoded string as required | 
| Decrypt | `E_DECRYPT_IV_DECODE` | The initialization vector value was not a base64 encoded string as required | 
| Decrypt | `E_DECRYPT_FAILED` | Decryption failed for the value found in the field | 
| Encrypt | `E_ENCRYPT_BAD_TYPE` | The value to encrypt must be a primitive type such as string, number, or boolean | 
| Encrypt | `E_ENCRYPT_FAILED` | Encryption failed for the value found in the field | 
| Event to Metric | `E_EVENT_TO_METRIC_FAILED` | The value(s) found in the event could not be coerced into a data type necessary for a metric (number, float, string) | 
| Filter | `E_COMPARE_COERCION_FAILED` | The comparison cannot be done because the value of the field cannot be coerced into the necessary type for comparison | 
| Filter | `E_COMPARE_BAD_CIDR` | The value found in the field does not appear to be a valid IP that can be used for CIDR comparison | 
| Filter | `E_COMPARE_BAD_TYPE` | The value of the field is an incompatible type for the requested comparison | 
| Flatten | `E_FLATTEN_BAD_TYPE` | The field to flatten contained a value that was not an object or array as required | 
| Parse | `E_PARSE_FAILED` | Parsing the field failed using the specified parser, which could be caused by a type mismatch | 
| Unroll | `E_UNROLL_BAD_TYPE` | The value found in the field was not an array as required | 
| **Source Errors** |  |  | 
| **Component** | **Error Code** | **Error Message** | 
| AWS Kinesis Firehose | `E_KINESIS_BAD_TYPE` | The field in the Kinesis Firehose payload was not an array as required | 
| AWS Kinesis Firehose | `E_KINESIS_BAD_JSON` | The Kinesis Firehose payload did not contain valid serialized JSON in the `.data` field of a record | 
| AWS Kinesis Firehose | `E_KINESIS_BAD_BASE64` | The Kinesis Firehose payload did not contain a correctly-encoded base64 string in the `.data` field of a record | 
| HTTP | `E_EVENT_NOT_JSON` | The payload was not valid serialized JSON, which is required | 
| HTTP | `E_EVENT_NOT_NDJSON` | The payload was not valid serialized NDJSON, which is required | 
| Mezmo Agent | `E_MEZMO_AGENT_BAD_TYPE` | The Mezmo Agent did not find an array of lines as required | 
| Splunk HEC | `E_SPLUNK_BAD_FORMAT` | The payload did not conform to the required format for Splunk HEC | 
| **General Errors** |  |  | 
|  | ``HTTP 413/REQUEST``ENTITY`` TOO LARGE`` | The payload exceeds 2MB | 
|  | `ERR_PLAN_EXCEEDED_PIPELINE_LIMIT` | You have exceeded the number of pipelines you are permitted to create for the plan you are on. | 
|  | `ERR_PLAN_EXCEEDED_NODE_LIMIT` | You have exceeded the number of nodes added to a pipeline for the plan you are on. | 
{% /table %}

{% /table %}