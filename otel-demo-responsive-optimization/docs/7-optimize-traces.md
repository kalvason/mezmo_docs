---
type: page
title: 7-optimize-traces
listed: true
slug: 7-optimize-traces
description: 
index_title: 7-optimize-traces
hidden: 
keywords: 
tags: 
---

---
title: Implement Trace Handling Pipeline for Downstream Tools
weight: 7
tags:
- Mezmo Pipeline
- OpenTelemetry
- OpenTelemetry Demo
- Metrics
- Aggregate
---

## Step 1: Create a new Pipeline to handle and route OpenTelemetry Traces

Create a new Mezmo Pipeline by clicking [New Pipeline](https://app.mezmo.com/pipelines/pipeline/new) in the platform.  Give this a name like `Trace Handler`.

## Step 2: Add OpenTelemetry Trace Source

Click `Add Source` and select your OpenTelemetry Trace source from the `Shared Sources` list similar to before.

## Step 3: Insert State Enrichment

Same as before, we will tee ourselves up for [Responsive Pipelines](https://docs.mezmo.com/telemetry-pipelines/configure-responsive-pipelines) in the future by enriching each trace with the current pipelines operational state.   Click the `three dots` on your Otel Trace Source and select `Add Node->Add Processor->Script Execution`.

Paste in the following Javascript and click `Save`.  Note that the script does a bit more than add the `operational_state` state variable by tagging this data in-flight.


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



## Step 4: Route Based on State

After the initial Enrichment processor, let's route the data flow based on that `operational_state`.  Connect a Route processor to the Enrichment Script with the following configuration:
* Title: `State Router`
* Route 1:
* Title: `Normal`
* Criteria: `message.op_state` `contains` `normal`
* Route 2:
* Title: `Incident`
* Criteria: `message.op_state` `contains` `incident`
* Route 3:
* Title: `Deploy`
* Criteria: `message.op_state` `contains` `deploy`

You will end up with a pipeline that looks like the following


{% image url="../../images/5-log-handler_state-router-config.png" caption="Trace State Router" %}
{% /image %}



## Step 5: Sample Traces in Normal State

Add a 1/10 Trace Sample processor connected to the Normal and Unmatched routes with the following configuration:
* Rate: `10`


{% image url="../../images/7-trace-handler_sample_config.png" caption="Trace Sample Config" %}
{% /image %}



{{% alert %}} Note that Tail based sampling is also available in Beta. {{% /alert %}}


## Step 6: Sending Data Downstream Systems

Now, connect all outputs to a Blackhole destination.  This is simply a placeholder for any Observability system you'd like.  Explore our destinations in-app or in our [docs](https://docs.mezmo.com/telemetry-pipelines/supported-telemetry-data-destinations) to easily send telemetry data downstream into tools, data lakes and more.


{% image url="../../images/7-trace-handler_blackhole_connected.png" caption="Trace Blackhole Connected" %}
{% /image %}



## Step 7: Deploy
Finally, you must deploy your pipeline in order to start exploring your log data.

## Step 8: Initiate State and Grab State ID
Same as with the Logs, let's initiate the State and save the `State ID` of this pipeline for later.

First, flip the State in the UX from Normal to Incident and back to Normal to initialize.

Then, in your terminal run run the following command with the metric `pipeline's ID` and grab that `State ID`.


{% code %}
{% tab language="bash" %}
curl --request GET \
 --url 'https://api.mezmo.com/v3/pipeline/state-variable?pipeline_id=PIPELINE_ID' \
 --header 'Authorization: Token PIPELINE_API_KEY'
{% /tab %}
{% /code %}



