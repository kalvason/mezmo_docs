---
type: page
title: Set Timestamp Processor
listed: true
slug: set-timestamp-processor
description: 
index_title: Set Timestamp Processor
hidden: 
keywords: 
tags: 
---


## Description

This Processor will allow you to override an event's timestamp with a field and parser of your choice. You can set multiple fields and parsers, and it will utilize the first one that successfully parses.

## Use

By default Mezmo Telemetry Pipelines set an event's `.timestamp`  field to the time that the event was received.  If your events already have a timestamp and you want to utilize that field for timestamp-related pipeline activities, you can use this Processor for that purpose.

## Configuration

{% table %}

{% table %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| Field | The JSON field to parse. | `.datetime` | 
| Timestamp Format | The [strftime](https://docs.rs/chrono/latest/chrono/format/strftime/index.html) format your timestamp is stored as.  There are several predefined timestamp formats.  You can also choose _Custom_, and define one of your own. | `%Y-%m-%dT%H:%M:%S` | 
{% /table %}

{% /table %}

## Examples

### Custom Event

If you have an event that stores its timestamp in a field called `.datetime` in a format like: `2022-01-10T05:15:40Z`


#### Before

{% code %}
{% tab language="json" %}
{
"level": "debug",
"eventname": "test",
"datetime": "2022-01-10T05:15:40Z"
}
{% /tab %}
{% /code %}

{% callout type="info" title="Message Only" %}
This  example affects  only the `.message` portion of the event.  The underlying event will also have `.metadata` and ``.timestamp`. ```You can use the [Pipeline Tap](/telemetry-pipelines/view-pipeline-data) feature to view these values for your source data.
{% /callout %}


#### Options

{% table %}

{% table %}
| Option | Value | 
| ---- | ---- | 
| Field | `.datetime` | 
| Timestamp Format | `%Y-%m-%dT%H:%M:%SZ` | 
{% /table %}

{% /table %}


#### After

(showing entire event, not just message)

{% code %}
{% tab language="json" %}
{
"messgage": {
"level": "debug",
"eventname": "test",
"datetime": "2022-01-10T05:15:40Z"
},
"metadata": {},
"timestamp": "2022-01-10T05:15:40.000000000+00:00"
}
{% /tab %}
{% /code %}