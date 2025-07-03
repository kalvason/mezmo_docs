---
type: page
title: Optimize Your Telemetry Data in Five Steps
listed: true
slug: optimize-your-observability-data-in-five-steps
description: 
index_title: Optimize Your Telemetry Data in Five Steps
hidden: 
keywords: 
tags: 
---

**Estimated Reading Time: 8 minutes**

## Introduction: Improving the ROI of Your Observability Data

Most observability tools rely on storage as the key metric for pricing, so if you want to reduce the cost of your observability data, you can start by focusing on the volume of data that you’re sending to storage. In this white paper, you’ll see how you can optimize your total observability spending with Mezmo Telemetry Pipelines by following five steps that can be applied to any log or metric data. 

## The Five Steps of Observability Data Optimization

1. **Filter** out duplicate and extraneous events that don’t contribute value to your observability results.
2. **Route** a full-fidelity copy of the remaining telemetry data to long-term retention solution for future auditing or investigation instead of your Observability tools.
3. **Trim and Transform** events by removing empty values, dropping unnecessary labels, and transforming inefficient data formats into a format specific to your observability destinations.
4. **Merge** events together  by grouping messages and combining their fields to retain unique data while removing repetitive data.
5. **Condense events into metrics** to reduce the number of hours and resources dedicated to supporting back-end tools, and convert unstructured data to structured before indexing to make searches more manageable, faster, and efficient.

## From Steps to Practice

Some of these steps may seem obvious, but they are not easy to put into practice. 

You can’t use an observability agent on its own to put these steps into practice. Agents are simply neutral forwarders, sending out information to be processed downstream in the observability analysis tools. 

You could implement some of these steps using open source tools and in-house development, but this comes with increased operational cost and complexity, requiring your team to build expertise that is not core to your business. 

Overall the main challenge with putting these steps into practice is that the available tools are either like agents, which simply send information, or like observability tools, which simply receive it. The need is to be able to process telemetry data in stream, to be able to transform and route it as it passes from agent to tool, to optimize and shape it for your downstream requirements. 

Our Mezmo Telemetry Pipelines were conceived with the goal of helping organizations get better control of their data in stream.This approach enables you to control the flow between your data sources and your observability tools, and manage in detail the optimization of your data before it arrives downstream.

## Putting the Five Steps into Practice

### 1: Filter

Noisy logs tend to make up a large percentage of overall data volume. Noise includes events such as positive confirmation signals, recurring process notifications, and repeated status values. For example, web logs often contain an abundance of status=200 messages that deduplication processing can remove. 

The key to filtering is being able to compare fields so you can determine whether a log is unique. If it is not unique outside of the timestamp, you should consider dropping it from the stream. If you need to keep the total number of logs that are non-unique, you can include that count in a representative log message.

You can use  our [Route](https://docs.mezmo.com/telemetry-pipelines/route-processor) and [Dedupe](https://docs.mezmo.com/telemetry-pipelines/dedupe-processor) processors with a configuration that ignores the timestamp as a way to handle noisy logs. Alternatively, you can choose which fields to match on explicitly if you need more criteria for duplication testing.

### 2:  Route

You may need to keep a portion of your logs in long-term retention with full-fidelity instances of telemetry data for compliance auditing or SRE troubleshooting. These logs can be routed to cold storage in the proper structure and rehydrated as necessary, without needing to be sent to your observability tools for operational monitoring.

Consider these criteria for routing logs to long-term storage:

- Audit logs or logs with user actions
- Logs that confirm a process starting or ending
- Non-essential operational metrics that may be needed for longer term performance analyzation, but not for short term operational monitoring

Mezmo’s [Route](https://docs.mezmo.com/telemetry-pipelines/route-processor) Processor intelligently routes data to cost-effective storage solutions, such as AWS S3. You can also configure the Route Processor to apply filtering options. For an example, check out our Pipeline example [Drop, Encrypt, and Route Data to Storage](https://docs.mezmo.com/telemetry-pipelines/pipeline-architecture-encryption) at [docs.mezmo.com](https://docs.mezmo.com).  

### 3:  Trim and Transform

A common situation is to have events where individual log lines have been packed with information because a lot of data has been dumped into one line within the application code. These events  can include stack traces and detailed data objects added for the purpose of debugging.

Large events typically have excess data in the message itself. Often this is unparsed data, though it is likely semi-structured. With Mezmo’s [Parse Processor](https://docs.mezmo.com/telemetry-pipelines/parse-process), you can use parsing techniques like regex or grok, to extract the important elements from the larger body and then remove the excess data. Stack traces, for example, can have the majority of the trace itself stripped out to retain only the originating source location. 

### 4: Merge

Firewall logs from systems like Palo Alto and AWS Firewalls generate a high volume of log events. Often these logs share a number of fields that are non-unique. However, you would not want to directly drop the logs due to the importance of the information from a security perspective.

With Mezmo’s [Reduce Processor](https://docs.mezmo.com/telemetry-pipelines/reduce-processor) you can merge multiple log input events into a single log event based on specified criteria. For example, Threat and Traffic logs from the firewall share 70% of the same fields, and are tied to the same events by a common sessionid field. 

### 5: Condense Events to Metrics

Beyond  reducing the volume of logs based on storage requirements, you should also  consider how you can optimize your operational insights to improve performance. This requires careful evaluation of the KPIs your teams are using to manage your infrastructure.

For example, you can use [the Mezmo Event to Metric Processor](https://docs.mezmo.com/telemetry-pipelines/event-to-metric-processor) to convert logs metrics and visualize them on an operational dashboard, providing valuable business insights while also helping reduce the inefficiencies that SRE teams and others have when accessing information they want.

[auto$](/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics) provides an overview of an event-to-metric Pipeline, along with information on Processor configuration. 

## Research and Findings

### Methodology

To test these techniques and substantiate our data reduction claims, we undertook  [a research project with our customer engineering and product team](https://docs.mezmo.com/practioner-guide-data-optimization/analysis-data-reduction-techniques)s. 

Data was collected from internal Mezmo sources where available to make it as close to representative of real world data as possible. Data collected from external sources was sourced from Kaggle.com and other open source locations, such as GitHub.

Data was then groomed via scripting as needed to flatten for loading into Snowflake. Each log schema was parsed and given its own table for storage and comparison.

In parallel, Telemetry Pipelines were created in a production environment with a standard account tied to the individual source types. Data was injected into each pipeline for each sample through an HTTP source.

Each pipeline attempted to follow the Snowflake queries, though variations in the technologies required some alterations.

Data samples sent into the pipeline were forwarded to HTTP destinations for comparison in the byte count from input to output.

Due to how pipelines and network layer traffic work, this naturally introduces variation versus the Snowflake analysis, so the results were not expected to match perfectly. However, these results more closely resemble real world cases because network layer translation would always be a part of any functioning log / metric system.

### Key Findings

The net findings are that following these steps can reduce the volume of telemetry data by **50% or more** without impacting your observability data, and that this is true across the many data sources we tested. 

- Using the **Filter** technique and dropping redundant events with deduplication criteria resulted in a **62% reduction from standard web logs such as Apache and nginx by matching based on the IP, URL, and request type**.
- Using the **Route** technique, we were able to separate more than 67% of Kubernetes logs by routing them to cold storage. 
- Using the **Trim and transform** technique, we were able to **reduce** **Kafka logs 50%** **by extracting common message data including process status updates, topic creation, and messages from the Controller.** Note that we still kept information fidelity in case it was needed for troubleshooting.
- Using the **Merge** technique, we were able to **reduce Firewall Log volume by 94% by removing unnecessary fields and grouping events based on source and destination IPs.**
- **Converting logs to metrics** can result in **over 90%** **reduction in total volume for all informational logs**, but the process must be carefully tuned to avoid the risk of losing potentially valuable data while avoiding an explosion of tag cardinality. Our Sales Engineering team can provide more information based on your data sources and observability needs. 

## Conclusion

By following the five steps described in this paper in the design of your Telemetry Pipeline, you can realize significant data optimization to reduce the cost of your observability data. If you want to know more about our research and findings, or to find out how our steps can be applied to your telemetry data, [reach out to our Solutions Engineering team](https://go.mezmo.com/schedule-a-demo?utm_medium=docs&amp;utm_source=docs-paid&amp;utm_campaign=practitioners-guide).