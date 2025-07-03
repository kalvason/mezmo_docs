---
type: page
title: Mezmo Log Analysis Ingestion
listed: true
slug: log-analysis-ingestion-source
description: 
index_title: Mezmo Log Analysis Ingestion
hidden: 
keywords: 
tags: 
---


## Description

This Source takes your data sent to our Log Analysis endpoint `logs.mezmo.com` and redirects it into a Pipeline Source.  This re-routes the data flow from Mezmo Log Management to your Pipeline.

There is no configuration for this source other than title and description.

{% callout type="error" title="Be Sure to Include a Mezmo Log Analysis Destination" %}
If you don't include a  [auto$](/telemetry-pipelines/mezmo-destination) Destination in the same Pipeline with this Source, you will no longer be sending data to the Log Analysis system, which will stop populating data for the log viewer and views/boards.
{% /callout %}

{% callout type="info" title="Single Source in Multiple Pipelines" %}
This Source can be used in multiple Pipelines.  If you delete all of your Mezmo Log Analysis Ingestion Sources, your data sent to logs.mezmo.com will then take their traditional route in the Log Analysis system. Check out the topic [auto$](/telemetry-pipelines/shared-sources) for more information.
{% /callout %}

### Supported Endpoints

At present, only four different ingestion endpoints at `logs.mezmo.com` are supported.

- `/logs/agent` : The endpoint our Mezmo Agents send their collected data to
- `/logs/ingest` : The endpoint many application plugins and custom apps send data to
- `syslog` : All syslog ingestion is supported in this source
- `heroku` : Heroku account log data is supported in this source