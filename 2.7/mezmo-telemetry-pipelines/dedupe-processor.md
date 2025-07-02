---
type: page
title: Dedupe Processor
listed: true
slug: dedupe-processor
description: 
index_title: Dedupe Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/dedupe-pipeline-processor#description)

The Dedupe processor removes duplicate values from log data.

## [Use](https://docs.mezmo.com/docs/dedupe-pipeline-processor#use)

This processor is most useful for reducing “chatter” in logs. The overlap of data across fields is the key to having this processor work effectively. This processor will emit the first matching record of the set of records that are being compared

## [Configuration](https://docs.mezmo.com/docs/dedupe-pipeline-processor#configuration)

There are three options to configure for this processor.

{% table widths="0,579" %}
| **Option** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Number of Events** | The number of events to compare across. Limited to 20000. | `5000` | 
| **Comparison Type** | **Match** will remove duplicate records based on the specified fields. \n\n\n\n**Ignore** will remove duplicate records based on all fields except those specified. | `Match` | 
| **Fields** | The field or fields to apply the Dedupe processing to. | `.foo` | 
{% /table %}

## [Example - Match](https://docs.mezmo.com/docs/dedupe-pipeline-processor#example---match)

### Before

{% code %}
{% tab language="json" %}
{"foo": "bar", "baz": 1}
{"foo": "bar", "baz": 2, 'bat': true}
{"foo": "qux", "baz": 3}
{"foo": "qux", "baz": 4}
{"foo": "qux", "baz": 5}
{% /tab %}
{% /code %}

### Dedupe Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| Number of Events | `5` | 
| Comparison Type | `Match` | 
| Fields | `.foo` | 
{% /table %}

### After

{% code %}
{% tab language="json" %}
{"foo": "bar", "baz": 1}
{"foo": "qux", "baz": 3}
{% /tab %}
{% /code %}

## Example - Ignore

### Before

{% code %}
{% tab language="json" %}
JSON
{"foo": "bar", "baz": 1}
{"foo": "bar", "baz": 2, "bat": true}
{"foo": "qux", "baz": 3}
{"foo": "qux", "baz": 4}
{"foo": "corge", "baz": 5}
{% /tab %}
{% /code %}

### Dedupe Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| Number of Events | `5` | 
| Comparison Type | `Ignore` | 
| Fields | `.baz` | 
{% /table %}

### After

{% code %}
{% tab language="json" %}
{"foo": "bar", "baz": 1}
{"foo": "bar", "baz": 2, "bat": true}
{"foo": "qux", "baz": 3}
{"foo": "corge", "baz": 5}
{% /tab %}
{% /code %}