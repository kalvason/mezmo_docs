---
type: page
title: Map Fields Processor
listed: true
slug: map-fields-processor
description: 
index_title: Map Fields Processor
hidden: 
keywords: 
tags: 
---

## Description

This processor enables you to move or copy fields within an event, including nested fields. 

## Use

You would typically use this processor for transformation of the data within an event, such as moving a nested field to the top level.

## Configuration

Specify the source and target fields where you want to move data. 

The default behavior is to copy the data to the specified target field from the source, and not overwrite the target field if it exists. If you want to remove the original field, set `Drop Source` as `true.`If you want to update an already-existing target field, set `Overwrite target` to `true`.

{% table widths="0,510" %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Source Field | The parsed data field from where the data to move originates. | `.data.host` | 
| Target Field | The field you want to move the data to. | `.hostname` | 
| Drop Source | Whether you want to remove the original field, or leave it as is (default is to leave as it is). | `True` | 
| Overwrite Target | Whether you want to override the target data if the field exists, or skip the map operation (default is to not overwrite) | `True` | 
{% /table %}

## Examples

### Restructuring

The initial log message from a database included `timestamp` and attribute information in nested objects. Additionally the `timestamp` field was not in a standard format.

#### Before

{% code %}
{% tab language="json" %}
{
  "t": {
    "$date": "2020-05-01T15:16:17.180+00:00"
  },
  "s": "I",
  "c": "NETWORK",
  "id": 12345,
  "ctx": "listener",
  "msg": "Listening on",
  "attr": {
    "address": "10.10.0.1"
  }
}
{% /tab %}
{% /code %}

#### Options

In this case you will shift the level of the date and move the address up a level, while also renaming the date field. You will specify to drop the originating value. You could optionally select to overwrite the destination if it exists, but it will not make a difference in this case.

{% table %}
| Option | Value | 
| ---- | ---- | 
| Move and remove the original value | `.t.$date` to `.timestamp` | 
| Move and remove the original value | `.attr.address` to `.address` | 
{% /table %}

#### After

{% callout type="info" title="Removing Objects with Remove Fields Processor" %}
Note that the originating objects still exist in the message. In this case, you would want to clean them up with a [auto$](/telemetry-pipelines/drop-fields-processor) following the Move.
{% /callout %}

{% code %}
{% tab language="json" %}
{
  "t": {},
  "timestamp": "2020-05-01T15:16:17.180+00:00"
  "s": "I",
  "c": "NETWORK",
  "id": 12345,
  "ctx": "listener",
  "msg": "Listening on",
  "address": "10.10.0.1"
  "attr": {}
}
{% /tab %}
{% /code %}