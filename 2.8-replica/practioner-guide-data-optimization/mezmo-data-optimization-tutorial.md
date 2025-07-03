---
type: page
title: Tutorial: Build a Telemetry Data Optimization Pipeline
listed: false
slug: mezmo-data-optimization-tutorial
description: 
index_title: Tutorial: Build a Telemetry Data Optimization Pipeline
hidden: 
keywords: 
tags: 
---


**Estimated Reading Time**: 10 minutes

## Overview

Using [Mezmo's data optimization techniques](/practioner-guide-data-optimization/optimize-your-observability-data-in-five-steps), you can reduce the volume of data that you send to your observability tools by as much as 50%. This not only saves you money by sending only the data you need to your tools, but can also save you from the tedious manual labor of data hygiene and maintenance required to make sure your data is optimized for your specific tools.

In this step-by-step tutorial, you'll learn how to:

- Build a telemetry data pipeline for the purpose of optimizing telemetry data for observability tools, using a sample of telemetry data Kafka logs
- Configure **Pipeline Processor**s to follow the five techniques for data reduction
- Use **Simulation Mode** and **Pipeline Taps** to test and verify the effect of Processors on your data stream
- Experiment with your own data on the Pipeline you create

## Architectural Overview

Your Pipeline will be based on the architecture described in [auto$](/practioner-guide-data-optimization/pipeline-architecture-for-data-reduction), and will utilize sample data from Kafka logs, as shown in the architecture overview. Once you have built this Pipeline and understand how the Processors relate to the five steps for data optimization, you can experiment with sending your own data through the Pipeline, and modifying the Processors and their configuration to meet your specific needs.

{% image url="https://uploads.developerhub.io/prod/2KW7/5yejxrgr5mjk88d2pc7karynoc50rmau7w1zt4qncn6kuelhk7yczg86ijf3p53k.png" mode="responsive" height="335" width="1207" %}
{% /image %}

## Create the Pipeline

In many cases, your logs will originate from one or more HTTP endpoints. In this step, you'll start with an [HTTP Source, ](/telemetry-pipelines/http-source) and add sample data based on Kafka logs to that source to test the Pipeline as you add Processors.

1. Log in to [the Mezmo Web App](https://app.mezmo.com). If you don't already have an account, you can [sign up for a 30 day trial](https://www.mezmo.com/sign-up-pipeline-today?utm_medium=docs&amp;utm_source=docs-paid&amp;utm_campaign=practitioners-guide).
2. Click the **Pipeline** icon in the left-hand navigation panel.
3. Click **New Pipeline,** enter a name for the Pipeline, and click **Save**.
4. At the bottom of the Pipeline Map, click **Add Source**.
5. Select **HTTP**,  but leave the configuration fields blank for now.
6. When the HTTP Source is added to the Pipeline Map, click on it open to open the contextual menu, and select **Edit Config**.
7. Under **Access Key Management**, click **Create New Key**.
8. Enter a **Title** for the key, then click **Create.**
9. Copy the Access Key, which you will use to send your own sample data through the Pipeline, as explained in the section **Experiment with Your Own Data.** Note that for security reasons you will not be able to see the key again after you save the configuration, and will need to generate new one if you don't have the original key. You should also make note of the API endpoint for sending Post requests to this Source.
10. Click **Update**.
11. Navigate to the[ Mezmo Log Sample repository on GitHub](https://github.com/mezmo/sample-data/tree/main/data), and download the **OpenTelemetry Kafka Demo Log** sample.
12. Click the HTTP Source node in the Pipeline Map, then click **Simulate Pipeline**.
13. Click **Create new sample**.
14. Use [the Python script in the sample library ](https://github.com/mezmo/sample-data/blob/main/scripts/send_file.py)to send the sample data to your HTTP source.
15. Enter a name for the data sample, then click **Save sample**.
16. Click the HTTP Source to confirm that the sample data is egressing as expected.

Your HTTP source will now have a data set you can work with to observe the effect of Processor transformations as the data moves through the Pipeline.

{% callout type="info" title="Chunking Your Files for the Max Request Size" %}
Note that the max limit per request is 2MB and the sample file size is larger than that. We recommend you chunk the file before sending it via any preferred method. If you would like to use a Python script to send, we have made available a sample script that does the chunking for you.
{% /callout %}

## Create the Blackhole Destinations

Before you add Processors, you should terminate your Pipeline with the **Blackhole Destination** that will drop all the data sent to it. This will enable you to view and experiment with your data in stream and understand how it will be appear when it reaches your production target Destination, without needing to work with live operational data. When you are satisfied with the results of your Processor chain, you can remove the Blackhole and [substitute a Destination](sfgsdfgsfg) that matches your production tools and storage.

{% callout type="info" title="Blackhole Best Practice" %}
A Blackhole Destination is not required for Pipeline operation, but it is good practice. If you don't connect a node to a destination, the data egressing from that node will be dropped and not shown as egress. Blackhole Destinations will show as non-billable egress.
{% /callout %}

For this example, you will create two Blackhole destinations, one that represents a **Metrics Consumer** tool, and another that represents a **Log Consumer** tool.

1. If you aren't already in Edit mode, click **Edit pipeline**.
2. In the Pipeline Map, click **Add Destination**.
3. Click **Blackhole**.
4. For **Title**, enter **Metrics Consumer,** then click **Save.**
5. Move your cursor over the right edge of the **HTTP Source** node until a blue circle appears, then drag the blue connector line to the right edge of the **Blackhole Destination** node. When the Blackhole node turns blue, click it to connect the Source and Destination.
6. Click **Deploy Pipeline**. You can only use **Simulation mode** and **Tap egress** with deployed Pipelines.
7. Click **Edit Pipeline** to return to edit mode.
8. Select the **HTTP Source** node, then click **Simulate**.
9. In the window that opens in the Pipeline Map, click **Run Simulation** next to the name of the sample.
10. Click the **HTTP Source**. You will see a display of the data that is egressing from it.
11. Click the **Blackhole Destination** node. You will see a display of the data that is ingressing to the node.
12. Click the **X-Close** in the bottom right of the Pipeline panel to exit Simulation mode.
13. Repeat steps 2 - 5 create the **Log Consumer Blackhole**.

As you add Processors to your Pipeline, you can run a simulation with the sample data to make sure that it is being processed as expected, and will be correctly optimized for your destination tools and storage.

## Filter and Deduplicate Data

The first step in any Data Optimization Pipeline is to filter out and deduplicate data, which can reduce the data sent through the rest of the Pipeline by as much as 50%. Typical examples of this type of data would included error and warning messages, process start and stop messages, and other routine log events like [200 Responses](/practioner-guide-data-optimization/filter-and-dedupe-200-responses). For this type of data engineering you could use the [auto$](/telemetry-pipelines/dedupe-processor), [auto$](/telemetry-pipelines/filter-processor), or [auto$](/telemetry-pipelines/parse-processor). In this case, you will set up the **Parse Processor** to identify and format log events based on a Grok pattern that parses the log timestamps, log levels, and descriptions.

1. In **Edit** mode, click the center of the blue line connecting the Source and Destinations, select **Insert processor**, then select **Parser** .
2. For **Parser**, select **Grok Pattern**.
3. For **Grok Pattern**, enter: `%{SQUARE_BRACKET}%{TIMESTAMP_ISO8601:timestamp}%{SQUARE_BRACKET} %{LOGLEVEL:level} %{GREEDYDATA:description}`
4. Open the **Test grok pattern** window and enter a section of the sample data to see the effect of the Parser.
5. Click **Save**.
6. Select the **HTTP Source**, then click **Simulate**.
7. Click **Run simulation**.
8. Click the **Parse Processor** to view the sample data ingressing and egressing the Processor.  Each time you add a Processor to your chain, you can check the effects of it on your data by using Simulation mode.

{% callout type="success" title="Parser Options" %}
The Parse Processor includes options for over a dozen different types of parsers, including Common Log, Grok Pattern, JSON, and RegEx.
{% /callout %}

{% callout type="success" title="Grok Pattern Reference" %}
The [auto$](/telemetry-pipelines/using-grok-to-parse) includes detailed information on how to create Grok patterns, as well as how to use special Mezmo Grok patterns, like `%{GREEDYDATA}`.
{% /callout %}

## Route Data

You can now route your parsed data to additional Processors or Destinations based on the data type. For this step you will use the [auto$](/telemetry-pipelines/route-processor) and conditional statements to separate data that should be sent to the **Metrics Consumer** from data that should be sent to the **Log Consumer**.

### Creating Routes

1. In edit mode, click **Add Processor**, then select **Route**.
2. Select the **Route** node, then select **Edit config**.
3. Click **Add Route**.
4. You will add four routes, with these names and conditional statements:

**Generating Records**

This statement matches the terms `generating` and `generated` in the `.description` field of the data.

{% code %}
{% tab language="none" %}
if (.description contains 'generating' OR .description contains 'generated')
{% /tab %}
{% /code %}

**Partition Management**

This statement matches the term `partition` in the `.description` field of the data.

{% code %}
{% tab language="none" %}
if (.description contains 'partition')
{% /tab %}
{% /code %}

**Error and Warnings**

This statement matches the terms `warn` and `error` in the .`level` field of the data.

{% code %}
{% tab language="none" %}
if (.level equal 'warn' OR 'error')
{% /tab %}
{% /code %}

**Deleted**

This statement matches the term `deleted` in the .`description` field of the data.

{% code %}
{% tab language="none" %}
if (.description contains 'deleted')
{% /tab %}
{% /code %}

When you have created all four routes, click **Save**. An additional route, **Unmatched**, is automatically created for all log datat that doesn't match one of the conditional statements.

### Connecting Routes

You can now connect each of the four routes to your Blackhole Destinations.

1. Connect the **Partition Management** and **Generating Records** routes to the **Metrics Consumer.**
2. Connect the **Errors & Warnings**, **Deleting Info**, and **Unmatched** routes to the **Log Consumer**.
3. Start Simulation mode.
4. Click each route in the **Route Processor** and select **Tap egress** to see the data that is egressing for that route.

## Condense Events into Metrics

Many log events, such as those concerning process start and stops, don't need to sent to your Log Consumer in full fidelity. The important information here is not in the individual events themselves, but in the aggregation of them into metrics that can provide you with insight into the operational load of these processes with your Metrics Consumer.

For this example, you can use the [auto$](/telemetry-pipelines/event-to-metric-processor) to create metrics for the **Generating Records** and **Partition Management** events, and then the [auto$](/telemetry-pipelines/aggregate-processor-deprecate) to aggregate them and pass them to the Metrics Consumer.

### Convert Generating Records Events to Metrics

1. In Edit mode, click **Add Processor**, and select **Event to Metric**.
2. Click **Edit Config**, and for **Title**, enter **Generating Records Events**.
3. For **Metric Name**, enter **generating_records**.
4. For **Kind**, select **Incremental.**
5. For **Type**, select **Counter**.
6. For **Value Type**, select **New value**.
7. For **Value**, enter **1**.
8. Under **Namespace**, for **Value Type**, select **None**.
9. Click **Save**.
10. Connect the Processor to the **Generating Records** route and the **Metrics Consumer Blackhole**.
11. Use Simulation mode and the Tap egress option to examine the events and the converted metrics.

### Convert Partition Management Events to Metrics

1. In Edit mode, click **Add Processor**, and select **Event to Metric**.
2. Click **Edit Config**, and for **Title**, enter **Partition Management Events**.
3. For **Metric Name**, enter **partition_management**.
4. For **Kind**, select **Incremental.**
5. For **Type**, select **Counter**.
6. For **Value Type**, select **New value**.
7. For **Value**, enter **1**.
8. Under **Namespace**, for **Value Type**, select **None**.
9. Click **Save**.
10. Connect the Processor to the **Partition Management** route and the **Metrics Consumer Blackhole**.
11. Use Simulation mode and the Tap egress option to examine the events and the converted metrics.

### Aggregate Event Metrics

1. In Edit mode, click **Add Processor,** and select **Aggregate (Metrics)**.
2. For **Title**, enter **Aggregate Process Metrics**.
3. For **Interval**, enter **10000**. This is the equivalent of a 10 second interval.
4. Click **Save**.
5. Connect the two **Event to Metric** Processors and the **Metrics Consumer Blackhole** to the Processor.
6. Use Simulation mode and the Tap egress option to examine the aggregated metrics.

{% callout type="success" title="Setting Time Intervals" %}
When setting time intervals for the **Aggregate** and **Reduce** Processors, you should consider how faithful you need to be to the original data to get the information you need. As a rule of thumb:

**30 seconds+** for low fidelity needs, ensuring positive affirmations

**10 seconds** for medium fidelity needs

**1 second** for high fidelity

**&lt; 1 second** for very high fidelity
{% /callout %}

## Merge Data

In your event data there will often be events where you want to preserve the information for the event, but merge similar events together to obtain a count of them. For example, firewalls often generate a large volume of Warning events, where you want to preserve the distinction between unique events, but merge information about similar events into a count of those events.

In this example, you can use the [auto$](/telemetry-pipelines/reduce-processor) to merge similar Warning events, while also maintaining a count of each type of Warning.

1. In Edit mode, click **Add Processor,** and select **Reduce**.
2. For **Title**, enter **Merge Warnings**.
3. For **Duration Milliseconds**, enter **30000**. This is the equivalent of 30 seconds.
4. Under **Merge Strategy per Field**, for **Field Path**, enter `.description`.
5. For **Merge Strategy**, select **Array**.
6. Click **Save**.
7. Connect the Processor to the **Warnings** route and the **Log Consumer Blackhole**.
8. Use Simulation mode and the Tap egress option to examine the merged events.

## Experiment with Your Own Data

Now that you've built a data optimization Pipeline and have been able to see the effects of the Processors on sample data, you can experiment with sending your own data to the Pipeline. Once you're satisfied with the results of the Processors, you can then remove the **Blackhole** destinations, and [set up a Pipeline Destination](/telemetry-pipelines/set-up-pipeline-destinations) for your own Log and Metrics consumers.

You could simply copy and paste your own sample data into the HTTP Endpoint Source, as you did with the provided sample data. However, a more efficient way to send your own sample data, and eventually your Production data, is with a `Curl` command. For this you will need to use the Access Key and API endpoint you set up in the first section of this tutorial.

Open a terminal window and enter this `Curl` command, substituting the API Endpoint URL and Access Key as shown in this example:

{% code %}
{% tab language="bash" %}
curl --data "&lt;LOG LINE&gt;" -H "Authorization: &lt;TOKEN&gt;" https://pipeline.mezmo.com/v1/&lt;ID&gt;
{% /tab %}
{% /code %}

This is an example of a complete command:

{% code %}
{% tab language="bash" %}
curl --data "[2023-06-06 11:37:14,430] INFO Deleted time index /var/lib/kafka/data/__cluster_metadata-0/00000000000003416804.timeindex.deleted. (kafka.log.LogSegment)" -H "Authorization: 5Q0plO8HGYzp+0uuLYz+UOhNIcKAKmnGrf9020ulO0k=" https://pipeline.mezmo.com/v1/29eb5cda-45ec-11ee-9dc0-fea009f4db67
{% /tab %}
{% /code %}

When you send the command, you will see a `200-OK` response, and the data stream graph at the top of the Pipeline Map will indicate that data is flowing to the Pipeline.

From here, you can begin to refine the configuration of the Processors, or add different ones, to engineer the data to meet your needs. Check out these topics in the documentation for more information about the Processors used in this tutorial, and others that you can use in your Pipeline.

- [auto$](/telemetry-pipelines/parse-processor)
- [auto$](/telemetry-pipelines/route-processor)
- [auto$](/telemetry-pipelines/event-to-metric-processor)
- [auto$](/telemetry-pipelines/aggregate-processor-deprecate)
- [auto$](/telemetry-pipelines/reduce-processor)
- [auto$](/telemetry-pipelines/filter-processor)
- [auto$](/telemetry-pipelines/dedupe-processor)

You can find details about all the Processors that are available for building Mezmo Telemetry Pipelines in the [auto$](/telemetry-pipelines/set-up-pipeline-processors) topics at [https://docs.mezmo.com](https://docs.mezmo.com).