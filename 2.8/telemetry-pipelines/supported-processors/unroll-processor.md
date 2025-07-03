---
type: page
title: Unroll Processor
listed: true
slug: unroll-processor
description: 
index_title: Unroll Processor
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/unroll-pipeline-processor#description)

The Unroll processor converts a JSON object array into individual objects.

## [Use](https://docs.mezmo.com/docs/unroll-pipeline-processor#use)

This processor is most commonly used for cases when a source sends a set of objects packaged in a single JSON object. This could include logs or metrics.

## [Configuration](https://docs.mezmo.com/docs/unroll-pipeline-processor#configuration)

There is one option to configure for this processor.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Field | The field containing the JSON object array to unroll. | .foo | 
{% /table %}

## Example

#### Before

{% code %}
{% tab language="json" %}
{
  'foo': ['bat', 'baz', 'qux'], 
  'bar': 1
}
{% /tab %}
{% /code %}

#### Unroll Options

{% table %}
| Option | Value | 
| ---- | ---- | 
| Field | .foo | 
{% /table %}

#### After

{% code %}
{% tab language="json" %}
{"bar": 1, "foo": "bat"}
{"bar": 1, "foo": "baz"}
{"bar": 1, "foo": "qux"}
{% /tab %}
{% /code %}