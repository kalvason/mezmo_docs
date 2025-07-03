---
type: page
title: Getting Started with the Mezmo Platform
listed: true
slug: getting-started-with-the-mezmo-platform
description: 
index_title: Getting Started with the Mezmo Platform
hidden: 
keywords: 
tags: 
---


Welcome to Mezmo! This Getting Started Guide will walk you through the process of setting up your organization, building your first telemetry pipeline, monitoring telemetry and creating alerts, and trying out the search and visualization features of Mezmo Log Analysis.

## Set Up Your Organization

When you created your Free Trial account, you also set up an Organization that you can add members to. This enables you to share reusable pipeline components like [auto$](/telemetry-pipelines/shared-sources) and  [Processor Groups](/telemetry-pipelines/create-processor-groups) with other members of your organization.

## Check out an Example Pipeline

For an example of specialized Pipeline for data optimization, check out the topic [auto$](/telemetry-pipelines/pipeline-architecture-for-kubernetes-data-optimizationzlz)

## Build Your First Pipeline

### Pipeline Basics

A Telemetry Pipeline is built from three components:

- Sources
- Destinations
- Processors

These topics will provide you with an introduction to each type of component, and a list of the component options for Mezmo Telemetry Pipelines, along with configuration instructions.

- [auto$](/telemetry-pipelines/set-up-pipeline-sources) and [auto$](/telemetry-pipelines/supported-telemetry-pipeline-sources)
- [auto$](/telemetry-pipelines/set-up-pipeline-processors) and [auto$](/telemetry-pipelines/supported-processors)
- [auto$](/telemetry-pipelines/set-up-pipeline-destinations) and [auto$](/telemetry-pipelines/supported-telemetry-data-destinations)

Our docs topic [auto$](/telemetry-pipelines/build-deploy-mezmo-pipeline) provides an overview of the basic Pipeline construction process, while [auto$](/telemetry-pipelines/view-pipeline-data) will explain how to view your pipeline data in-stream and create samples to use in testing your pipeline.

### With Mezmo Flow

With [Mezmo Flow](/telemetry-pipelines/about-mezmo-flow) guiding the way, you can set up your first log volume reduction pipeline in minutes! Set up your data source, then let Mezmo Flow profile your data and make recommendations for processors to reduce your log volume by as much as 50%.


#### Add a Data Source

The first step is to set up the Source of your telemetry data. Your options include using the [auto$](/telemetry-pipelines/mezmo-agent-source), an [auto$](/telemetry-pipelines/otel-collector), or [auto$](/telemetry-pipelines/demo-logs-source) You can find a complete list of  [auto$](/telemetry-pipelines/supported-telemetry-pipeline-sources) in our product documentation.

{% synced id="datadogflow" %}
{% /synced %}


#### Create a Profile

A [Data Profile](/telemetry-pipelines/data-profiling) provides you with an in-depth analysis of the most common types, volume, and sources of your incoming telemetry data. When you set up a Source with Mezmo Flow, you will generate a data profile for that source.

When the data profiler completes its analysis, you’ll see charts that provide you with information about the composition of the source logs, the most common message patterns, and a breakdown of log metrics by app, host, level, and log type.


#### Add a Data Destination

All telemetry pipelines terminate in a Destination like an observability tool or a storage location. When you set up a Pipeline using Mezmo Flow, [auto$](/telemetry-pipelines/log-analysis-source) is automatically added as a Destination. You can find [a complete list of supported Destinations](/telemetry-pipelines/supported-telemetry-data-destinations) in our product documentation.


#### Add Processors

Once Mezmo Flow has analyzed your data and presented you with a data profile, you have the ability to apply Processors to specific message patterns to reduce the volume of log data you’re sending to your destination.

1. Select the Processor you want to apply to the log data from the **Process Logs** menu.
2. As you select a Processor, you will see the effect it has on your overall log volume.
3. When you’re satisfied with the results, click **Apply Processors to Pipeline**.
4. Mezmo Flow will generate a visualization of your Pipeline, with your selected processors grouped into a [Processor Group](/telemetry-pipelines/create-processor-groups).
5. You can now edit your Pipeline, add or edit the configuration of the components, or set up additional functionality like [auto$](/telemetry-pipelines/in-stream-alerts). Just click **Edit Pipeline** to get started.
6. When you’re finished working on your Pipeline, don’t forget to click **Deploy** to make the changes active!

You can find a complete list of the available processors, along with links to configuration instructions and usage information, on our [auto$](/telemetry-pipelines/supported-processors) page.

If you need more information or advice on building a telemetry pipeline to meet your data management requirements, feel free to reach out to our Technical Services team!

### Learn with a Tutorial

These tutorials, which include interactive demos, will show you how to build a mini-pipeline, also known as a Pipette, for specific processing functionality. Along the way you’ll learn about best practices like using the [auto$](/telemetry-pipelines/blackhole-destination) destination for testing, using [Pipeline Tap](/telemetry-pipelines/tap-and-view-edge-data) to view the changes in data as it passes along the Processor chain, and using [Simulationn Mode](/telemetry-pipelines/simulate-pipeline-data-flows) to test the end-to-end processing of your data.

- [Tutorial: Convert Events to Metrics](/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics)
- [Tutorial: Mask and Encrypt Data](/practioner-guide-data-optimization/pipeline-module--security-and-compliance)
- [Tutorial: Route Data](/practioner-guide-data-optimization/pipeline-module--route)

## View and Analyze Telemetry Data

Once you’ve set up your telemetry data pipeline with a Mezmo Log Analysis Destination, you can use the log viewing and search functionality to take a deep dive into your optimized data.

- [Configure Mezmo Log Analysis](/telemetry-pipelines/mezmo-destination)
- [auto$](/docs/view-log-data)
- [auto$](/docs/searching-log-contents)

## Create Alerts

One of the most important features of a telemetry data platform is its ability to notify you of critical system conditions in a timely way. With most observability tools, alerts are sent only after the data has been indexed and analyzed, which can have a significant negative impact on your ability to respond.

With the Mezmo Platform, you can set alerts not only for the volume of data being indexed, as well as specific views, you can also set alert conditions for any data stream in your telemetry pipeline, which will alert you within milliseconds of the event occurring, rather than after it has been indexed.

- [auto$](/docs/create-index-rate-alerts)
- [auto$](/docs/add-alerts-to-views)
- [auto$](/docs/usage-alerts)
- [auto$](/telemetry-pipelines/pipeline-threshold-alerts)
- [auto$](/telemetry-pipelines/set-in-stream-alerts)

## Visualize Telemetry Data

With Mezmo's Log Management visualization features, you can create graphs that will enable you to track trends in your log data over time.

- [auto$](/docs/visualize-log-data-with-graphs)