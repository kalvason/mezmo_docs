---
type: page
title: About Mezmo Flow
listed: true
slug: about-mezmo-flow
description: 
index_title: About Mezmo Flow
hidden: 
keywords: 
tags: 
---


Mezmo Flow provides an easy onboarding experience focused on helping you gain an understanding of your data, and then recommending Processors based on common patterns and message types. With Mezmo Flow, you're four steps away from creating a telemetry data Pipeline that will substantially reduce the volume of telemetry data sent to your storage locations and observability tools, saving both on costs and the mental toil required to optimize your data for your observability requirements.

1. Mezmo Flow begins when you [create your organization](/docs/organization-management-overview) in the Mezmo Web App, and then [set up a Data Source](/telemetry-pipelines/supported-telemetry-pipeline-sources) to start sending your data to Mezmo. Mezmo Flow will also automatically set up [auto$](/telemetry-pipelines/mezmo-destination) as the data Destination for your Pipeline.
2. As the telemetry data from your Source is ingested, the [Data Profiler](/telemetry-pipelines/data-profiling) will analyze it and present you with an overview of the most common message patterns, and metrics for the apps and hosts that are generating the most log data.
3. From there you can select [Processors ](/telemetry-pipelines/supported-processors) to apply to message patterns, and see the way in which each Processor affects the reduction of your overall log volume.
4. When you're satisfied with the results, you can apply your selected Processors to the telemetry data, and Mezmo Flow will generate a Pipeline that includes your selected Processors.

Once your Pipeline is active, you can use the [Pipeline Tap](/telemetry-pipelines/view-pipeline-data) feature to examine the transformations to the data in stream and make changes to the Processor configurations as needed. Your Pipeline will also include the [Data Profiler Processor](/telemetry-pipelines/data-profiler-processor) that you can use to examine your data profile, or generate a new one after making changes to your Source or your Processor configurations.

{% synced id="datadogflow" %}
{% /synced %}

## Interactive Demo

This interactive demo shows the process of creating a data profile with Mezmo Flow. You need to have pop-ups enabled to view the demo. You can also [view the demo without pop-ups ](https://www.mezmo.com/demos/interactive-demo-mezmo-flow)at mezmo.com

{% html %}
&lt;!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page --&gt;
&lt;button data-navattic-open="https://capture.navattic.com/cm369qz3m000203l24myv8f3a" data-navattic-title="Mezmo Flow Demo"&gt;
View the demo in a pop-up
&lt;/button&gt;
{% /html %}