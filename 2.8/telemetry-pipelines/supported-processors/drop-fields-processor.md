---
type: page
title: Remove Fields Processor
listed: true
slug: drop-fields-processor
description: 
index_title: Remove Fields Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/remove-fields-pipeline-processor#description)

The Remove Fields processor drops JSON fields from each record in the data stream.

## [Use](https://docs.mezmo.com/docs/remove-fields-pipeline-processor#use)

This processor is useful when there are specific fields that you want to remove from your data before sending it to storage or to additional processors.

## [Configuration](https://docs.mezmo.com/docs/remove-fields-pipeline-processor#configuration)

There is one option to configure for this processor.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Fields | The field or fields to drop from each record in the data stream. | `.baz` | 
{% /table %}

## [Example](https://docs.mezmo.com/docs/remove-fields-pipeline-processor#example)

### Before

{% code %}
{% tab language="json" %}
{
  "foo": "bar",
  "baz": 1
}
{% /tab %}
{% /code %}

### Remove Fields Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| Fields | `.baz` | 
{% /table %}

### After

{% code %}
{% tab language="json" %}
{
  "foo": "bar"
}
{% /tab %}
{% /code %}