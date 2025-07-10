---
type: page
title: 6 - Create an OpenTelemetry Metric Handler Pipeline
listed: true
slug: 6---optimize-metrics
description: 
index_title: 6 - Create an OpenTelemetry Metric Handler Pipeline
hidden: 
keywords: 
tags: 
---

{% synced id="workshop-need-help" %}
{% /synced %}

In this step you will create a responsive pipeline to handle the OpenTelemetry metrics data. 

## Pipeline Architecture

This schematic shows the architecture of the Pipline you will create in this stop. The numbers in the schematic correspond to the step in the build process. 

{% image url="https://uploads.developerhub.io/prod/2KW7/vcwybagsiq6u93xd6v6nwabwsy0ipu3fuxy81wkpujksryzd5nhiolvx2mj1mml5.png" mode="responsive" height="622" width="3342" %}
{% /image %}

## 1 - Create the Pipeline and Add the Source

1. In the Mezmo Web app, click **New Pipeline** and name it `Metric Handler`. 
2. In the Pipeline Map, click **Add Source**, then select the OpenTelemetry Metric source you created in Step 2. 

## 2 - Add State Variables

A responsive pipeline changes its functioning based on detection of state changes. For this example, you will use the [auto$](/telemetry-pipelines/js-script-processor) to add variables to the data that indicate the operational state of the pipeline. 

1. Click the `...`menu in the upper-right corner of the OpenTelemetry Metric source. 
2. Select **Add Node &gt; Add Processor &gt; Script Execution.**
3. Copy and paste this script into the **Script** field in the processor configuration panel, then click **Save**. 

{% code %}
{% tab language="javascript" %}
function processEvent(message, metadata, timestamp, annotations) {
  const state = getPipelineStateVariable("operational_state")
  message.op_state = state
  
  message.name = message.name.toString()
  message.tags.op_state = state

  metadata.resource.attributes["pipeline.path"] = "with_mezmo"

  if( message == null ){ return null }
  
  return message
}
{% /tab %}
{% /code %}

## 3 - Route Data Based on State

You can now set the Pipeline to route data based `on operational_state` with the [auto$](/telemetry-pipelines/route-processor).

1. **In the Pipeline Map, click Add Processor.** 
2. Select **Route Processor,** and for **Title**, enter `State Router`. 
3. You will create three routes, one for the `Normal` state, one for the `Incident` state, and one for the `Deploy` state. After you configure the options for the `Normal` state, click **Add route** to configure the `Incident` and `Deploy` routes. 

### Normal Route Configuration

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Title** | `Normal` | 
| **Conditional Statement** | `if message.op_state contains normal` | 
{% /table %}

### Incident State Configuration

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Title** | `Incident` | 
| **Conditional Statement** | `if message.op_state contains incident` | 
{% /table %}

### Deploy State Configuration

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Title** | `Deploy` | 
| **Conditional Statement** | `if message.op_state contains deploy` | 
{% /table %}

## 4 - Create the Metric Data Optimization Processor Chain

In normal functioning, a common approach to reducing metric volume is to aggregate metrics and reduce tag cardinality. In this step, you will connect a Script Execution Processor, a [auto$](/telemetry-pipelines/metrics-tag-cardinality-limit-processor), and an [auto$](/telemetry-pipelines/aggregate-processor), in that order, to the normal and unmatched routes of the Route Processor. 

### Script Execution Processor Configuration

1. In the Pipeline Map, add a Script Execution Processor to the Pipeline, and connect it to both the unmatched and normal routes. 
2. Copy and paste this script into the processor configuration. 

{% code %}
{% tab language="javascript" %}
function processEvent(message, metadata, timestamp, annotations) {

  let service_name = message.tags.service_name
  let host_id = message.tags.host_id
  
  if( service_name == null ){
    service_name = metadata.resource.attributes['service.name']
  }
  if( service_name == null ){ service_name = 'NA' }
  if( host_id == null ){
    host_id = metadata.resource.attributes['host.id']
  }
  if( host_id == null ){ host_id = 'NA' }

  message.tags = {
    'service_name': service_name,
    'host_id': host_id
  }
  
  return message
}
{% /tab %}
{% /code %}

### Tag Cardinality Limit Processor Configuration

This configuration will limit the number of tags for the `host_id field` to 10. 

1. In the Pipeline Map, add a Tag Cardinality Limit Processor and connect it to the Script Execution Processor. 
2. Enter these configuration options for the processor. 

{% table widths="" %}
| Configuration Option | Setting | 
| ---- | ---- | 
| **Tags** | `message.tags.host_id` | 
| **Action** | `drop_tag` | 
| **Value Limit** | `10` | 
| **Mode** | `Probablistic` | 
{% /table %}

### Aggregate Processor Configuration

This configuration will aggregate metrics based on a five mintue interval. 

1. In the Pipeline Map, add an Aggregate Processor and connect it to the Tag Cardinality LImit Processor. 
2. Keep the default configuration setttings, but set **Interval (seconds)** to `300`. 

## 5 - Add the Blackhole Destination

You can send your optimized data to any of Mezmo's [auto$](/telemetry-pipelines/supported-telemetry-data-destinations), but in this case, the route will terminate in a [auto$](/telemetry-pipelines/blackhole-destination) destination that drops all data sent to it. This is useful for testing the data processing of your Pipeline before sending it to production destination. 

1. In the Pipeline Map, click **Add Destination**. 
2. Select **Blackhole**, and connect it to the to outgoing routes of the Route Processor as shown in the pipeline architecture schematic. 

## Deploy the Pipeline

To activate the Pipeline, click **Deploy**. 

## Initiatalize State and Get State ID

As you did with the Log Hander Pipeline, you need to intialize the state of the Pipeline and get the `State ID` of the pipeline for reference in Step 8.

1. In the Pipeline Map, click on the **State** setting in the upper-left corner, and change it to `Incident`.
2. Change the **State** setting back to `Normal`. This will initialize the Normal state, and generate the`Pipeline_ID` for the pipeline `state-variable`. 
3. In a terminal, run this command with the 

First, flip the State in the UX from Normal to Incident and back to Normal to initialize.

Then, in your terminal run run the following command with the metric `pipeline's ID` and grab that `State ID`.

{% code %}
{% tab language="bash" %}
curl --request GET \
 --url 'https://api.mezmo.com/v3/pipeline/state-variable?pipeline_id=PIPELINE_ID' \
 --header 'Authorization: Token PIPELINE_API_KEY'
{% /tab %}
{% /code %}