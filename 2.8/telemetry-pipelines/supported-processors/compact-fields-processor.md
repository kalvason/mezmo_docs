---
type: page
title: Compact Fields Processor
listed: true
slug: compact-fields-processor
description: 
index_title: Compact Fields Processor
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/compact-fields-pipeline-processor#description)

Removes all nested fields recursively that contain empty arrays or objects from a specified field. This processor includes options to remove values from Arrays, and from Objects.

## [Use](https://docs.mezmo.com/docs/compact-fields-pipeline-processor#use)

This processor is particularly useful in cleaning up null values and other empty spaces within messages.

## [Configuration](https://docs.mezmo.com/docs/compact-fields-pipeline-processor#configuration)

There are two options to configure for this processor.

{% table %}

{% table %}
| **Option** | **Description** | Example | 
| ---- | ---- | ---- | 
| **Fields** | The field or fields to remove empty values from | . | 
| **Compact Options** | Select to enable Compact for Arrays in the field, Objects in the field, or both | On / Off | 
{% /table %}

{% /table %}

## [Example](https://docs.mezmo.com/docs/compact-fields-pipeline-processor#example)

### Before

{% code %}
{% tab language="json" %}
{
"baz": [],
"foo": "bar",
"quux": {
"corge": {},
"grault": 1
},
"qux": {}
}
{% /tab %}
{% /code %}

### Compact Options

{% table %}

{% table %}
| **Option** | **Value** | 
| ---- | ---- | 
| Field | . | 
| Compact Array | On | 
| Compact Object | On | 
{% /table %}

{% /table %}

### After

{% code %}
{% tab language="json" %}
{
"foo": "bar",
"quux": {
"grault": 1
}
}
{% /tab %}
{% /code %}