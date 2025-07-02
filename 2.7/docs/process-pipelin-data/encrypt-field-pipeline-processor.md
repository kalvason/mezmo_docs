---
type: page
title: Encrypt Field Processor
listed: true
slug: encrypt-field-pipeline-processor
description: 
index_title: Encrypt Field Processor
hidden: 
keywords: 
tags: 
---

## Description

You can use the Encrypt processor to apply an encryption algorithm and key to a specified field.

## Use

The Encrypt processor is useful when you need to send sensitive log data to storage, for example when you want to retain log data that may contain account names and passwords. 

## Configuration

There are four options you need to set for this processor. 

{% table %}
| **Option** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Field** | The field you want to apply encryption to. | `.foo` | 
| **Encryption algorithm** | The encryption algorithm to apply. These options also determine how many characters to use for the encryption key and initialization vector. | `AES-256-CFB (key=32 characters, iv=16characters)` | 
| **Encryption key** | The key used by the algorithm to encrypt the field. | `6B58703273357638792F423F4528482B` | 
| **Initialization vector (IV) field** | This field is added by the pipeline to the JSON and is used by the algorithm as the initialization key. | .`encrypt_iv` | 
{% /table %}

## Example

**Before**

{% code %}
{% tab language="json" %}
{
  "foo": "bar"
}
{% /tab %}
{% /code %}

**Encryption Options**

{% table %}
| **Option** | **Value** | 
| ---- | ---- | 
| Field | .foo | 
| Encryption algorithm | AES-256-CFB (key=32 characters, iv=16characters) | 
| Encryption key | 6B58703273357638792F423F4528482B | 
| Initialization vector (IV) field | .encrypt_iv | 
{% /table %}

**After**

{% code %}
{% tab language="json" %}
{
  "encrypt_iv": "FmXUb0OPOWm1A2kw6diKYw==",
  "foo": "vFza"
}
{% /tab %}
{% /code %}