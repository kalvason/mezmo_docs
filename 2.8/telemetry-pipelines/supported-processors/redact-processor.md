---
type: page
title: Redact Processor
listed: true
slug: redact-processor
description: 
index_title: Redact Processor
hidden: 
keywords: 
tags: 
---

## Description

With this Processor you can identify and redact Personally Identifiable Information (PII) in your data stream. This includes items like:

- Social Security numbers
- Email addresses
- Credit cards
- Phone numbers

This Processor identifies PII based on pattern detection. When the specified pattern is detected, you have the option to replace it with a specified string, or use a standard hash. When using this Processor in a [auto$](/mezmo-edge/mezmo-edge-pipelines-for-local-data), you can also specify a regular expression to use for pattern detection.  

## Configuration

{% table widths="104,0" %}
| Option | Description | Example/Options | 
| ---- | ---- | ---- | 
| **Title** | A title for the processor | Redact SSN | 
| **Description** | A description of the Processor's function in the Pipeline | Replaces SSNs with a text string | 
| **Field (Optional)** | The field to search for the pattern. If the field is not specified, the Processor will look for the pattern across all the fields. | `Message` | 
| **Mask Pattern** |  |  | 
|  | **Pattern** | Credit card number\n\n\n\nEmail address\n\n\n\nIPv4 address\n\n\n\nUS or Canada phone number\n\n\n\nUS social security number\n\n\n\nCustom Regex Pattern ([auto$](/mezmo-edge/mezmo-edge-pipelines-for-local-data)only) | 
|  | **Action** | Hash\n\n\n\nReplace\n\n\n\nDetect Only | 
|  | Hash Options\n\nThe value is hashed and base64 encoded | md5\n\n\n\nsha1\n\n\n\nsha2 (sha2-512_256)\n\n\nsha3 (sha3-512) | 
|  | Replacement | &lt;Any text string&gt; | 
| **PII Presence** | When pre-set or custom PII patterns are detected in an event, a metadata field will be added to the event that can be used by down stream processors for collecting metrics or [trigger an alert](/telemetry-pipelines/presence-of-personally-identifying-information--pii-) that this pattern is present. Metadata field will indicate one or more PII patterns detected in the event as shown below:\n\n\n"pii_presence": {\n\n\n\n"email_address": "yes",\n\n\n\n        "us_social_security_number": "yes"\n\n\n\n      }\n\n\n\nIf no PII patterns are detected,  _pii_presence_ field will not be added to the metadata. | On or Off | 
{% /table %}

### Pre-defined Patterns

#### Social Security Number

The US social security number pattern matches any valid social security number sequence, with or without optional delimiters.

Examples:

- XXX YY ZZZZ
- XXX-YY-ZZZZ
- XXX YY-ZZZZ
- XXX-YY ZZZZ
- XXXYYZZZZ

#### Phone Number

The phone number pattern matches valid phone numbers, with or without space, hypen or period (.) delimiters.

Valid phone numbers include:

1. +1 XXX YYY ZZZZ
2. +1 (XXX) YYY ZZZZ
3. +1.(XXX).YYY.ZZZZ
4. +1XXXYYYZZZZ
5. +1-XXX YYY.ZZZZ, etc. .

The matcher will also match parts of sequences (false positives). Partially matched phone numbers includes:

1. XXX.YYY.ZZZZ will be matched in the input +1_XXX.YYY.ZZZZ
2. XXX.YYY.ZZZZ will be matched in the input +1.MXXX.YYY.ZZZZ

#### Credit Card Number

The credit card pattern currently matches Visa, Mastercard, American Express, Diners club and JCB card numbers.

**Visa**

13 to 16 digit numbers starting with 4. Examples: 4XXXXXXXXXXXX or 4XXXXXXXXXXXXXXX

**Mastercard**

16 digit numbers starting with 21-27 (new range) or 51-57 (old range).

Examples: 21XXXXXXXXXXXXXX or 56XXXXXXXXXXXXXX

**American Express (AMEX)**

15 digit numbers starting with 34 or 37. Examples: 34XXXXXXXXXXXXX or 37XXXXXXXXXXXXX

**Diners Club**

14 digit numbers starting with 300-305 or 360-389. Examples: 300XXXXXXXXXXX or 389XXXXXXXXXXX

**JCB**

15 digit numbers starting with 2131 or 1800 or 16 digit numbers starting with 35. Examples: 2131XXXXXXXXXXX.

### Email Address

Matches RFC 5322 compliant email addresses.

Examples: [user@dummy.com](mailto:user@dummy.com), [user@127.0.0.1](mailto:user@127.0.0.1), etc

## Interactive Demo

Check out an interactive demo of the Redact Processor as a component in [a Compliance group](/practioner-guide-data-optimization/pipeline-module--security-and-compliance), as well as instructions for building a version of the Pipette with your own sample data. 

## Examples

### Redact Social Security Number with String

{% table %}
| Option | Value | 
| ---- | ---- | 
| Pattern | US social security number | 
| Action | Replace | 
| Replacement | 000-00-000 | 
{% /table %}

### Redact Social Security Number to Hash

{% table %}
| Option | Value | 
| ---- | ---- | 
| Pattern | US social security number | 
| Action | Hash | 
| Hash | md5 | 
{% /table %}

### Custom Regex Example: Redact Canadian Social Security Number

{% table %}
| Option | Value | 
| ---- | ---- | 
| Pattern | Custom | 
| Action | Replace | 
| Expression | (?&lt;ssn_canada&gt;(\d{3})-(\d{3})-(\d{3})) | 
| Replacement | 111-111-111 | 
{% /table %}

### Redact Email Address to String

{% table %}
| Option | Value | 
| ---- | ---- | 
| Pattern | Email address | 
| Action | Replace | 
| Replacement | [someone@nowwhere.com](mailto:someone@nowwhere.com) | 
{% /table %}