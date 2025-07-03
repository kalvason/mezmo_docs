---
type: page
title: Decrypt Field Processor
listed: true
slug: decrypt-fields-processor
description: 
index_title: Decrypt Field Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/decrypt-field-pipeline-processor#description)

This processor decrypts a single encrypted string using a defined secret as well as a specified Initialization Vector (IV) field. 

## [Use](https://docs.mezmo.com/docs/decrypt-field-pipeline-processor#use)

Typically you would use the Decrypt processor to remove the encryption applied by the Encrypt processor.

## [Configuration](https://docs.mezmo.com/docs/decrypt-field-pipeline-processor#configuration)

The Decrypt processor uses the same configuration options as the Encrypt processor.

{% table %}
| **Option** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Field** | The field you want to decrypt. | `.foo` | 
| **Encryption algorithm** | The encryption algorithm to apply. These options also determine how many characters to use for the encryption key and initialization vector. | `AES-256-CFB (key=32 characters, iv=16characters)` | 
| **Encryption key** | The key used by the algorithm to encrypt the field. | `6B58703273357638792F423F4528482B` | 
| **Initialization vector (IV) field** | This value is used by the algorithm as the initialization key. | .`encrypt_iv` | 
{% /table %}

## [Example](https://docs.mezmo.com/docs/decrypt-field-pipeline-processor#example)

### Before

{% code %}
{% tab language="json" title="" %}
{
  "encrypt_iv": "FmXUb0OPOWm1A2kw6diKYw==",
  "foo": "vFza"
}
{% /tab %}
{% /code %}

### Decryption Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| Field | `.foo` | 
| Decryption algorithm | `AES-256-CFB (key=32 characters, iv=16characters)` | 
| Decryption key | `6B58703273357638792F423F4528482B` | 
| Initialization vector (IV) field | `.encrypt_iv` | 
{% /table %}

### After

{% code %}
{% tab language="json" %}
{
  "encrypt_iv": "FmXUb0OPOWm1A2kw6diKYw==",
  "foo": "bar"
}
{% /tab %}
{% /code %}