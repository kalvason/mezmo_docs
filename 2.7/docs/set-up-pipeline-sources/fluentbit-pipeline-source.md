---
type: page
title: FluentBit
listed: true
slug: fluentbit-pipeline-source
description: 
index_title: FluentBit
hidden: 
keywords: 
tags: 
---

## Description

You can stream FluentBit logs and metrics to Mezmo Pipelines.

## Configuration

To send your FluentBit data to a Mezmo Pipeline, you will need to edit the `Output` section of the FluentBit configuration file as shown in this example:

{% code %}
{% tab language="none" %}
Ouput
    Name          forward
		Match         *
		  # update these to point to your Mezmo Pipeline instance
		Host          127.0.0.1
		Port          443
{% /tab %}
{% /code %}

### Mezmo Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| Decoding Method | The decoding method to use to convert frames to data events. | 
{% /table %}