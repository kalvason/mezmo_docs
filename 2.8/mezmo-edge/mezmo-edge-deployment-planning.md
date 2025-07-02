---
type: page
title: Mezmo Edge Deployment Planning
listed: true
slug: mezmo-edge-deployment-planning
description: 
index_title: Mezmo Edge Deployment Planning
hidden: 
keywords: 
tags: 
---


Mezmo Telemetry Pipeline is built as a cloud-native SaaS application. For cases where processing data within your environment is a requirement, we created Mezmo Edge.

Mezmo Edge lets you run a telemetry data pipeline with the same functionality available in Mezmo Cloud, but locally hosted within your own environment. All of the metrics and management of the pipelines on your Edge instance are still handled by the Cloud infrastructure.

Mezmo Edge can be deployed to any Kubernetes cluster using a Helm chart, as described in the topic [auto$](/mezmo-edge/set-up-mezmo-edge-in-kubernetes).

## Key Deployment Considerations

1. **Data ingestion**: how much data are you planning to send through Edge?
2. **Processing requirements**: are you planning to do any special processing, such as regex, deduplication, or other custom scripts?
3. **Destination targets**: where are you planning to send the data?

## Deployment Model

Mezmo Edge uses a hybrid cloud deployment model. When the Edge satellite nodes are deployed they automatically contact the Mezmo Cloud APIs. For this reason, Edge currently requires access to the wide area network (WAN) to function.

{% image url="https://uploads.developerhub.io/prod/2KW7/dl22in5wrtv9ejucw9l9g1nv7caj9wsmf1jqlja6pg7ig3g6arpygshneeq2m9vf.jpg" mode="full" height="445" width="1053" %}
{% /image %}

## Resource Requirements

These numbers are intended for general guidance. Resource requirements depend on many factors. Use the deployment considerations in combination with the sizing guidance to estimate actual sizing.

### Sizing

These numbers are effective averages to use in approximation. Your individual event sizes may. Estimations in events per second (EPS) are conservative. These specifications are based on the guidelines published in[ the Vector documentation.](https://vector.dev/docs/setup/going-to-prod/sizing/#estimations)

Assumptions

1. Each vCPU is a standard ARM processor without hyperthreading
2. Throughputs are purposefully conservative

{% table %}

{% table %}
| Event Type | Typical Use Case | Typical Event Size | Expected Trhoughput | Event Throughput | 
| ---- | ---- | ---- | ---- | ---- | 
| Unstructured Log | Parsing, processing, and routing to an external destination | 256 bytes | ~10 MiB/s/vCPU | ~40k EPS/vCPU | 
| Structured Log | Processing and routing to an external destination | 1 kilobyte | ~25 MiB/s/vCPU | ~25k EPS/vCPU | 
| Metric | Aggregation and routing to an external destination | 256 bytes | ~25 MiB/s/vCPU | ~100k EPS/vCPU | 
{% /table %}

{% /table %}

## Recommendations

Recommendations are divided based on small, medium, and large size deployments. For most use cases, a medium size deployment is sufficient.

{% table %}

{% table %}
| Deployment Size | Typical Use Case | Expected Event Throughput | Guidance Specifications | 
| ---- | ---- | ---- | ---- | 
| Small | Parsing and routing to an external destination | 40-80k EPS\n\n\n\n\n&lt;1 TB/day | 2 vCPUs\n\n\n\n\n\n\n\n4GB of memory | 
| Medium | Parsing common unstructured log types, moderate processing, sending to multiple external destinations | 100k-200k EPS\n\n\n\n\n1 - 5 TB/day | 4 vCPUs\n\n\n\n\n\n\n\n8GB of memory | 
| Large | PII redaction, parsing with regex, processing, and sending to multiple external destinations | 200k-400k EPS\n\n\n\n\n5 TB/day + | 8 vCPUs\n\n\n\n\n\n\n\n16GB of memory | 
{% /table %}

{% /table %}

### Disk Space

Disk buffering is not currently in use within Edge. Disk space is not a bottleneck in terms of performance. High performance disks or over provisioned disk space will only add to cost, with no performance benefit.

### High Availability

High availability can be achieved by using a separate hot failover instance. **We do not recommend this configuration**. If you need to have high availability, we recommend using our Cloud infrastructure.

## Performance Considerations

### Parsing

Parsing well structured logs, such as JSON, has a minimal impact on overall utilization. Parsing unstructured logs of known formats into structured logs does utilize CPU resources, though not heavily. Regex or grok parsing can require increased resource utilization, especially when event sizes are larger than average.

If you plan on doing heavy parsing, consider targeting a higher deployment size.

### Processing

Most transformations are highly efficient and cause minimal CPU load. Regex routing can require significantly increased CPU resources, especially if the event sizes are larger than average.

For deduplication, reduction, and aggregation, the buffer size necessitates dedicated memory in order to process. Make sure to err on the conservative side for memory allocation if you’re planning to include these processors.

### Destinations

As you add more destinations, the buffering required for sending data to each one increases the total memory load. The I/O operations also utilize CPU to send the packets.

If you plan to add many destinations, or duplicate data to multiple destinations, keep in mind that the resource requirements may increase, primarily in terms of memory.

## Autoscaling

### Vertical Scaling

Normal recommendations are to allow for vertical scaling of your Edge instance. This ensures that your data stream remains unaltered. No changes to configuration are needed for this to take effect.

### Horizontal Scaling

There is an option to turn on horizontal pod scaling within the helm configuration. The standard Kubernetes autoscaling will divide up the workload across the pods, typically allocating in a round robin fashion, depending on how you’ve configured your cluster. However, note that as you add pods and split the workload, certain features like Reduce, Aggregate, and Dedupe may be affected due to the splitting of the event stream across the nodes.

## Durability

Durability within Edge is currently limited to end-to-end acknowledgement of events reaching their destination. By default, acknowledgements are on for destinations that support it.

If durability is a requirement for your data, you can send the events to the Mezmo Cloud environment, which has built-in durability by default, and then onto the end destination.

Mezmo does not collect any of the event data passing through the pipelines. If you use the [Tap](/telemetry-pipelines/simulate-pipeline-data-flows) feature, we will open a tap into the data stream and route that data through our cloud environment. We do not save any of the tapped data. Tapped data persists in your browser cache for a limited period of time.

Mezmo does collect metrics regarding the total data throughput and total events passing through every Edge instance. We collect this information for billing purposes as well as to provide monitoring and troubleshooting.

**If you block the metrics we collect, your Edge instance may cease to function and process data.**

## Sensitive Data

If you are passing sensitive data through your pipeline, keep in mind that while we do not receive this data, tapping a Pipeline with this data could result in sensitive data passing through the Mezmo Cloud and appearing in the browser.

If you want to send data from an Edge Pipeline to a Cloud Pipeline, you can do so with our [auto$](/telemetry-pipelines/http-source) Processor as a destination and source respectively. Note that the metadata, such as any query parameters or headers from your initial Edge ingestion, must be persisted into the payload if you want to keep that intact for later use in the Cloud Pipeline.