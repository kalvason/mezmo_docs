---
type: page
title: Types of Telemetry Data Pipelines
listed: true
slug: types-of-telemetry-data-pipelines
description: 
index_title: Types of Telemetry Data Pipelines
hidden: 
keywords: 
tags: 
---

In the Mezmo O'Reilly Report [_The Fundamentals of Telemetry Pipelines_](https://www.mezmo.com/resources/oreilly-report-the-fundamentals-of-telemetry-pipelines), telemetry data is described as a raw resource that must be refined in order to become useful information. The process of refinement is carried out through a telemetry pipeline. There is, however, no one-size-fits-all approach to telemetry pipeline design - you must design the pipeline to produce the type of information that suits your purpose. 

While the word "pipeline" brings to mind images of pipes, valves, and other plumbing fixtures, a data pipeline is better thought of as an algorithm - a series of operations executed in a spedific order to produce a result. Within a telemetry data pipeline, the operations are represented by processors or processor groups that perform specific functions. 

In this guide you'll find examples of Mezmo Telemetry Pipelines that are designed for specific purposes, along with descriptions of the processors typically used in each type of pipeline. You will also find tutorials for  building "Pipettes" using [Mezmo Demo Source Data](/telemetry-pipelines/demo-logs-source), and interactive demos to help you understand how data is transformed into information as it passes through the pipeline. 

## Data Ingestion Pipelines

Data ingestion pipelines are designed to send log data to Mezmo Log Analysis. 

{% table widths="207" %}
|  |  | 
| ---- | ---- | 
| [auto$](/guide-to-pipeline-architecture/basic-log-analysis-pipeline) | This pipeline is designed to optimize data before it is sent to Mezmo Log Analysis. In this case, you would tailor the optimization processes to your specific data type, as shown in the **Data Optimization Pipelines** section. The tutorial shows you how to send source data directly to Mezmo Log Analysis, and then view the live tail of that data. | 
| [auto$](/guide-to-pipeline-architecture/log-analysis-source-pipeline) | This pipeline was originally designed to provide users of the Mezmo Log Analysis product with a migration path to the Mezmo Platform. | 
{% /table %}

## Data Optimization Pipelines

Data optimization pipelines are designed to optimize specific types of data before sending it to observability tools and storage. These pipelines typically use processors like [Filter](/telemetry-pipelines/filter-processor), [Route](/telemetry-pipelines/route-processor), [Event to Metric](/telemetry-pipelines/event-to-metric-processor), and [Aggregate](/telemetry-pipelines/aggregate-processor) to transform the data into the format required for the destinations. The [Mezmo Data Profiler](/telemetry-pipelines/data-profiler-processor)  can help you [understand your data](/guide-to-pipeline-architecture/understanding-your-data-to-optimize-it) and provide recommendations for how to optimize it. 

{% table widths="" %}
| Example Pipelines | Description | 
| ---- | ---- | 
| [auto$](/guide-to-pipeline-architecture/basic-data-optimization-pipeline) | A basic pipeline to demonstrate the typical data optimization operations. | 
| [auto$](/guide-to-pipeline-architecture/kafka-data-optimization-pipeline) | A pipeline designed to optimize Kafka data. | 
| [auto$](/guide-to-pipeline-architecture/kubernetes-data-optimization-pipeline) | A pipeline designed to optimize Kubernetes data. | 
| [auto$](/guide-to-pipeline-architecture/nobl9-data-optimization-pipeline) | A pipeline designed to optimize data for observing Service Level Objective (SLO) and Service Level Indicator (SLI) metrics in Nobl9 | 
{% /table %}

## Data Archiving and Rehydration Pipelines

Data archiving and rehydration pipelines are designed to optimize data for storage by reducing its volume, but then being able to restore or "rehydrate" it as needed for incident or other investigations. The archiving pipeline will typically include elements of a [auto$](/guide-to-pipeline-architecture/basic-log-volume-reduction-pipeline), as well as processors to [auto$](/guide-to-pipeline-architecture/mask-and-encrypt-data) in situations in which the data potentially includes Personally Identifying Information (PII). The rehydration pipeline will typically include processors like [Filter](/telemetry-pipelines/filter-processor) and [Map Fields](/telemetry-pipelines/map-fields-processor), to make sure the data is in the correct format for your log analysis tool. 

{% table widths="" %}
| Example Pipelines | Description | 
| ---- | ---- | 
| [auto$](/guide-to-pipeline-architecture/basic-data-rehydration-pipeline) | A basic set of archive and rehydration pipelines to show typical components, and how to create a restoration task. | 
{% /table %}

## Responsive Pipelines

Responsive pipelines are designed to change the pipeline's data processing operations when a defined condition is detected in the data, for example a surge in data from a particular source, or the detection of PII data. This enables you to preserve full-fidelity copies of your data during an incident, for example, and is intended to help you reduce Mean Time to Resolution (MTTR). These pipelines use Mezmo's [auto$](/telemetry-pipelines/in-stream-alerts) feature, as well as processors like [Script Execution](/telemetry-pipelines/js-script-processor) and [auto$](/telemetry-pipelines/reduce-processor).

{% table widths="" %}
| Example Pipelines | Description | 
| ---- | ---- | 
|  |  | 
|  |  | 
{% /table %}

## Cost Reduction Pipelines

Cost reduction pipelines are designed to reduce the overall volume of your telemetry data that your send to storage or observability tools like Datadog, and thereby reduce your telemetry data management costs. You can use [Mezmo Flow](/telemetry-pipelines/about-mezmo-flow) to understand which elements of your data are important to preserve, and then generate a pipeline that will preserve the important information while filtering out the noise. 

{% table widths="" %}
| Example Pipelines | Description | 
| ---- | ---- | 
|  |  | 
|  |  | 
{% /table %}

## Data Standardization Pipelines

Data standardization pipelines can be pipelines that are built for any purpose, but use Mezmo features like [auto$](/telemetry-pipelines/shared-sources) and [Processor Groups](/telemetry-pipelines/create-processor-groups) to standardize the source data and processing components across the teams in your organization. 

{% table widths="" %}
| Example Pipelines | Description | 
| ---- | ---- | 
|  |  | 
|  |  | 
{% /table %}