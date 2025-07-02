---
type: page
title: Unroll Processor
listed: true
slug: unroll-pipeline-processor
description: 
index_title: Unroll Processor
hidden: 
keywords: 
tags: 
---

## Description

The Unroll processor converts a JSON object array into individual objects.

## Use

This processor is most commonly used for cases when a source sends a set of objects packaged in a single JSON object. This could include logs or metrics. 

## Configuration

There is one option to configure for this processor.

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Field | The field containing the JSON object array to unroll. | .foo | 
{% /table %}

## Example

**Before**

{% code %}
{% tab language="json" title="JSON" %}
{
  'foo': ['bat', 'baz', 'qux'], 
  'bar': 1
}
{% /tab %}
{% /code %}

**Unroll Options**

{% table %}
| Option | Value | 
| ---- | ---- | 
| Field | .foo | 
{% /table %}

**After**

{% code %}
{% tab language="json" %}
{"bar": 1, "foo": "bat"}
{"bar": 1, "foo": "baz"}
{"bar": 1, "foo": "qux"}
{% /tab %}
{% /code %}

 

**Before**

{% code %}
{% tab language="json" %}
[
  {'foo': 'bar', 'bat': 1}, 
  {'foo': 'bar', 'bat': 2}, 
  {'foo': 'bar', 'bat': 3}
]
{% /tab %}
{% /code %}

**Unroll Options**

{% table %}
| Option | Value | 
| ---- | ---- | 
| Field | . | 
{% /table %}

**After**

{% code %}
{% tab language="json" %}
{'foo': 'bar', 'bat': 1}
{'foo': 'bar', 'bat': 2}
{'foo': 'bar', 'bat': 3}
{% /tab %}
{% /code %}