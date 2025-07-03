---
type: page
title: Create a Data Profile
listed: true
slug: data-profiling
description: 
index_title: Create a Data Profile
hidden: 
keywords: 
tags: 
---


## What is Data Profiling?

The Data Profiling feature of Mezmo Telemetry Pipelines enables you to gain a deep understanding of the types, volume, and sources of your incoming telemetry data.

## Create a Data Profile

There are two ways to generate a data profile:

1. As part of the [Mezmo Flow](/telemetry-pipelines/about-mezmo-flow) onboarding process.
2. Through the [Data Profiler Processor](/telemetry-pipelines/data-profiler-processor), which is added to your pipeline as part of the Mezmo Flow process, or you can set it up as a component within a Pipeline that you build yourself.

## View the Data Profile

Once a Data Profile has been generated for the Source, you can access it through both the Processor itself, and the navigation in the Mezmo Web App.

{% image url="https://uploads.developerhub.io/prod/2KW7/256x1stbrp1yjnas1wgpdzo9raamuqmvm5su3izvjh3zh65aezv901xk1yu0w92c.png" mode="responsive" height="1606" width="2882" %}
{% /image %}

Data profiler analyzes the streaming telemetry using multiple techniques so that users have better insights based on the type of telemetry. Analysis of the telemetry is organized in three different tabs in the report and explained below: **Message Templates,** **Field Summaries**, and **Log Metrics.**

Message templates provide better insights into logs that are textual in nature, where as Field Summaries provide better insights into structured data such as JSON longs.

### Message Templates

**The Message Templates** section provides a report of log patterns discovered in the data.  This enables you to understand how much specific log patterns contribute to the overall source volume, expressed as a percentage of the total data volume. With this information, you can determine if the logs matching the pattern are important for investigation and troubleshooting , or if they are low-value logs that can be archived and don't need to be sent to your observability platform.

The columns in the Message Templates section, which are all sortable, include:

- **Apps,** which shows the number of apps that produced these log patterns. You can hover on the number to see the name of the app(s) that produced the log pattern.
- **Template** shows the tokenized log lines with variables that change from message to message, such as IP or Host, and are replaced by`<*>`
- **Total Lines** shows the number of log lines that match this pattern
- **Total Line Size** shows the sum of all the log lines that match this pattern

You can see examples for each matching log sample by clicking the arrow next for each of the message templates.

{% image url="https://uploads.developerhub.io/prod/2KW7/n4ne4gy3m4qwyy6ekyolxr8nw5p4ovka0ehe6nj915goelfeg5zz0e840mt4dcro.png" caption="The Message Templates discovered by the Data Profiler, including the app that generated the selected template, and matching log samples" mode="responsive" height="1414" width="1465" %}
{% /image %}

### Field Summaries

{% synced id="experimentalbanner" %}
{% /synced %}

Field summaries provide the analysis of telemetry data from the perspective of field values.  The Field Summaries section provides a tabular view of all the Fields discovered from the events that are streaming through the pipeline during a profiler run. Click the arrow next to the field name to see the unique values  associated with the field. You can also apply Processors to those unique values.

Within the Field Summaries report, you will see:

{% table widths="" %}

{% table %}
| Report Column | Description | 
| ---- | ---- | 
| **Field Name** | The name of the field. | 
| **Unique Values** | Represents the count of the unique values found in all the logs during the profiling run. This indicates the cardinality of the field. Some fields can have a large number of unique values, however, the report will only display the first 500 unique values. The value displayed depends on the type of field, as described in the next table. | 
| **Total Lines** | Similar to the message templates, this column shows:\n\n\n\n\n\n\n\nThe number of log events that contain this field.\n\n\n\n\n\n\n\nThe percentage of logs that contain this field. The Percentage is calculated based on the total volume of data processed by the profiler during that specific run. | 
| **Total Size** | Similar to the message templates, this column shows:\n\n\n\n\n\n\n\n**S**ize of all the events containing this field.\n\n\n\n\n\n\n\nThe number of events containing this field. | 
| **Field Size** | This represents the volume contributed by the **field itself** as Bytes and % of the total volume. It includes the field name and value.  Using this information, you can decide to drop a field if it contains a large amount of data that is not important. | 
{% /table %}

{% /table %}

You can also apply Processors based on **Field** or **Field Value**. At the **Field** level, you can  can only select Remove Field. At the **Field Value** level, you can apply Processors such as [Filter](/telemetry-pipelines/filter-processor), [auto$](/telemetry-pipelines/sample-processor),  [auto$](/telemetry-pipelines/dedupe-processor), and [auto$](/telemetry-pipelines/throttle-processor). If you remove a field at the Field level,  the Field Value processors are disabled because they are mutually exclusive.

This table describes the value displayed based on the value type:

{% table widths="" %}

{% table %}
| Value Type | Displayed Value | 
| ---- | ---- | 
| **Boolean** | The value itself. | 
| **String** | The value itself, up to the first 50 characters. | 
| **Array** | The length of the arrays found. For example, `[a, b, c]` is displayed as **3**. | 
| **Object** | Each unique value is the set of names of the keys. For example,`{a:1, b:2}` is displayed as **a, b**. | 
| **Float** | Displays the min/max/average, no unique values. | 
| **Timestamp** | Displayes the min/max (no average), no unique values | 
| **Integer** | If cardinality is &gt; the threshold (for example, 65), displays min/max/average. If cardinality is &lt; threshold, displays the unique values. | 
{% /table %}

{% /table %}

{% image url="https://uploads.developerhub.io/prod/2KW7/yw4nzl6ibf4zl1lxgee5m4p319he3lqzf7y7zr8uve9g71c6ypfu8kexknyh6wdb.png" caption="Field Summaries generated by the Data Profiler, showing the Unique Values associated with the `app` field." mode="responsive" height="1054" width="1456" %}
{% /image %}

### Log Metrics

The **Log Metrics** section provides a report of the profiled logs categorized by **App**, **Host**, **Log Level** and **Log Type**:

{% image url="https://uploads.developerhub.io/prod/2KW7/ij9u9fei9i0mg47vnm7ze269kmmbc4u3d1ptu9zhoygmaoree1wh643zql7r2cm8.png" caption="The Log Metrics analysis for an HTTP Shared Source" mode="responsive" height="802" width="1942" %}
{% /image %}

###