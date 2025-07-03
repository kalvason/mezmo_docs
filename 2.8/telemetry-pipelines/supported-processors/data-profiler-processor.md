---
type: page
title: Data Profiler Processor
listed: true
slug: data-profiler-processor
description: 
index_title: Data Profiler Processor
hidden: 
keywords: 
tags: 
---

## Description

The Data Profiling Processor analyzes Source data and presents an overview of the most common message patterns, as well as the apps and hosts, contributing to the overall log volume.  

## Use

A Data Profiling Processor is automatically added to your Pipeline as part of the [Mezmo Flow](/telemetry-pipelines/about-mezmo-flow) process, but can also be added to a Pipeline as an independent component. Typically you connect all your source data to a Profiler so that it can analyze all the data. 

For the Data Profiler to work effectively, it needs to know which fields in the log line correspond to a `Host`, `App`, `Label` or `Level`. The Data Profiler provides configuration options to map these fields. This mapping mechanism may not work for all log formats. If the log format is drastically different and these fields cannot be mapped using the Data Profiler configuration, you can use a [auto$](/telemetry-pipelines/map-fields-processor) for example, to reshape the logs so the Data Profiler can process and categorize the log patterns correctly. In this case, you should  add the Profiler processor after the Map Fields Processor in the Pipeline, or after any processors meant to transform the logs.

If you make changes to your upstream Source or any of the Processor configurations, you can then use the Data Profiling Processor to re-analyze the data and generate a new profile.

Once you have applied Processors to the log data in the profile and generated a Pipeline, the **Actions** for that profile will be disabled, and you will not be able to change the applied Processors. If you want to generate a new Pipeline, run the Profiler again, and apply Processors as necessary. 

{% callout type="info" title="Profiler Run Time" %}
Profiler will run its analysis until it reaches 1M lines or has run for 24 hours.
{% /callout %}

## Configuration

The Data Profiling Processor analyzes your log data and categorizes the discovered log patterns based on `App`, `Host`, `Label` or `Level` field values. This helps you to understand which Apps contributed to a log pattern. However, different source logs can have different names for these fields. For example, some sources may have and `App` field  while other sources may have a `Service` field to indicate the App or Service. Similarly, some logs may have a `Line` field, while other sources may have a `Message` field. 

You can configure the Data Profiler to normalize the paths for your app and host names, as well as log levels and lines, as shown in these configuration options. The Profiler looks for the existence of any of these fields to normalize the data for analysis. 

{% table widths="" %}
| Option | Description | Example | 
| ---- | ---- | ---- | 
| App Path(s) | The paths to fields containing application names. | `.app .service` | 
| Host Path(s) | The paths to fields containing host names. | `.host .hostname` | 
| Level Path(s) | The paths to fields containing log levels. | `.level` | 
| Line Path(s) | The paths to fields containing log lines. | `.lines .message` | 
{% /table %}

## View the Data Profile

Once a Data Profile has been generated for the Source, you can access it through both the Processor itself, and the navigation in the Mezmo Web App. Check out [auto$](/telemetry-pipelines/data-profiling) for more information on the reports created for the profile. 

If you want to generate a new data profile for the Processor, access the current data profile, then click **Reset Profile.** The Data Profiler will  then run a new analysis of your log data. 

If you run the Data Profiler multiple times without resetting, any new log templates that are discovered will be added to the existing report. 

{% image url="https://uploads.developerhub.io/prod/2KW7/7dwws3aqx3ka7hiclwzdi0uoavyfm6etcd696l0r1xzpxq3hiemyljf3acrajgtg.png" caption="This screenshot shows how to access the Data Profile for a Pipeline through both the Processor and the navigation in the Mezmo Web App." mode="responsive" height="1606" width="2882" %}
{% /image %}