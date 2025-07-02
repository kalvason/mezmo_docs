---
type: page
title: Flatten Fields Processor
listed: true
slug: flatten-field-pipeline-processor
description: 
index_title: Flatten Fields Processor
hidden: 
keywords: 
tags: 
---

## Description

This processor recursively reduces the level of a set of objects and appends the prior level to the keys of each.

## Use

The flatten processor is useful when you need all nested fields of a JSON object to be moved to a single level.  This can be beneficial when integrating with a system that can't handle complex or nested data.

## Configuration

There are two options for configuring this processor.

{% table %}
| **Option** | **Description** | **Example** | 
| ---- | ---- | ---- | 
| **Fields** | The field or fields to flatten. | `.foo` | 
| **Flatten Options** | Specify the delimiter to use for combining field names with the flattened data. | _ | 
{% /table %}

## Examples

**Before**

{% code %}
{% tab language="json" %}
{
  "foo": {
    "bar": {
      "baz": 1,
      "qux": "quux"
    },
    "corge": [
      1,
      2,
      3
    ]
  }
}
{% /tab %}
{% /code %}

**Flatten Options**

{% table %}
| Option | Value | 
| ---- | ---- | 
| **Field** | .`foo` | 
| **Delimiter** | _ | 
{% /table %}

**After**

{% code %}
{% tab language="json" %}
{
  "foo_bar_baz": 1,
  "foo_bar_qux": "quux",
  "foo_corge": [
    1,
    2,
    3
  ]
}
{% /tab %}
{% /code %}