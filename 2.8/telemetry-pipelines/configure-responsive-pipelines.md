---
type: page
title: Configure Responsive Pipelines
listed: true
slug: configure-responsive-pipelines
description: 
index_title: Configure Responsive Pipelines
hidden: 
keywords: 
tags: 
---

{% callout type="info" title="Beta" %}
This feature is in Beta development. For access to this feature, contact your Mezmo Account Manager, or reach out to our Solutions Engineering team for more information.
{% /callout %}

Responsive Pipelines enable you to pre-configure a Pipeline to change behavior automatically in the case of an incident. This makes it easier to balance the need for high-fidelity data required during incident response, with the need to reduce data load for cost reduction.

Responsive Pipelines adjust their behavior in response to specific triggers, such as the detection of a new critical incident. State change can be triggered through API calls from external incident response systems, such as PagerDuty, or you can activate it manually in the Pipeline in the [Mezmo Web App](app.mezmo.com). 

{% image url="https://uploads.developerhub.io/prod/2KW7/h4jmec50zi3hfvmvok9dxlnap2l9iwwmehqyheahz3trg08amqkp7kscqqzvod18.png" mode="responsive" height="477" width="1219" %}
{% /image %}

This screenshot shows a Pipeline that, in **Monitoring** mode, drops `Status 200` events, and converts other HTTP Status events to metrics. In **Incident** Mode, the Route Processor sends the full data stream to Mezmo Log Analysis. 

## Beta Limitations

The Beta release of Responsive Pipelines has these limitations:

- You need to use the  [auto$](/telemetry-pipelines/js-script-processor) to access the pipeline state variable and add it to the event metadata as described below.
- You can only change the Pipeline operational state via the Mezmo Telemetry Pipelines API

## How it Works

Mezmo Responsive Pipelines introduces a state variable `operational_state` that is associated with each Pipeline. The value for this state is either `normal`or `incident`, and the Processors in the Pipeline can change their functioning based on the value. For example, the **Sample** Processor can be disabled if `operational_state=incident` so that during the incident, you can have high fidelity data for further analysis. 

## Set the Pipeline Operational State

You can change  the operational state of a Pipeline manually through the Mezmo Web App,  or through the Telemetry Pipelines API. 

### Mezmo Web App

You can change the operational state of a Pipeline in the Mezmo Web App by selecting the state in the upper-left corner of the Pipeline Map. The state of the Pipeline is also shown in the Pipeline name, with an orange flag indicating the **Incident** state. 

{% image url="https://uploads.developerhub.io/prod/2KW7/pt5iwjtqwchdc01qpcxnbq117svndul3xe9yk91voub7983l9p0zz7zegmikmbm1.png" caption="Changing the operational state of a Pipeline in the Mezmo Web App" mode="300" height="495" width="300" %}
{% /image %}

{% callout type="info" title="Change State in the Web App to Initialize State Table" %}
You should change the state of a Pipeline in the Mezmo App at least once to initialize the Pipeline's state table so it can be used  with the API.
{% /callout %}

### Script Execution Processor

You can use the [auto$](/telemetry-pipelines/js-script-processor)  to add the operational state of a Pipeline as metadata to a message  to change the functioning of downstream Processors, such as the [auto$](/telemetry-pipelines/route-processor).

This code shows how to get the Pipeline state variable and set it as message metadata for downstream Processors:

{% code %}
{% tab language="none" %}
function processEvent(message, metadata) {
const state = getPipelineStateVariable("operational_state")
message.op_state = state
return message

}
{% /tab %}
{% /code %}

{% image url="https://uploads.developerhub.io/prod/2KW7/40gfiueor5pb549yep90zvsk3w7o91nmljiy6luqfkphydprkqscm18h4vkztzn5.png" caption="This screenshot shows the configuration  of the Script Execution Process to get the operational state of a Pipeline and use it in a message for downstream Processors" mode="responsive" height="639" width="1038" %}
{% /image %}

You can these use the value of `op_state` to set the routing conditions for the Pipeline, as shown in this example:

{% code %}
{% tab language="none" %}
Route Processor Configuration

<Normal State>
if (metadata._op_state equal 'normal' OR is_null(metadata._op_state))

<Incident State>
if (metadata._op_state equal 'incident')
{% /tab %}
{% /code %}

{% image url="https://uploads.developerhub.io/prod/2KW7/whbmfgiai2ok2ahywhgjgf733i7odvhbu2alv8wil8px9k1dzvlcr6eybqtdd8my.png" caption="This screenshot shows the configuration of the conditions in the Route Processor for both Monitoring and Incident Modes" mode="full" height="605" width="1000" %}
{% /image %}

### API

You can get and set the value of the Pipeline operational state with the Telemetry Pipelines API:

Get the `state_id`:

{% code %}
{% tab language="none" %}
curl -s --request GET --url https://api.mezmo.com/v3/pipeline/state-variable -H 'Authorization: Token <<PIPELINE_SERVICE_TOKEN>>' -H 'Content-Type: application/json' --data '{"pipeline_id": "<<PIPELINE_ID>>"}' | jq '.data[0].state'
{% /tab %}
{% /code %}

Set the state:

{% code %}
{% tab language="none" %}
curl -i --request PUT --url https://api.mezmo.com/v3/pipeline/state-variable/<<STATEID>> -H 'Authorization: Token <<PIPELINE SERVICE_TOKEN>>' -H 'Content-Type: application/json' --data '{"pipeline_id": "<<PIPELINE_ID>>", "state": {"operational_state": "incident"}}'
{% /tab %}
{% /code %}

## Interactive Demo

This interactive demo illustrates a telemetry pipeline that is configured to respond to a Datadog data volume spike incident. You will need to have pop-ups enabled to view the demo. You can also [view the demo without pop-ups](https://www.mezmo.com/demos/responsive-pipeline-volume-spike) at mezmo.com

{% html %}
<!-- To open the pop-up on clicking a button, add the following data-navattic attributes to an existing button on your page -->
<button data-navattic-open="https://capture.navattic.com/clzsclm8e000009laaj3zeyyn" data-navattic-title="Responsive Pipeline: Volume Spike Protection">
  View the demo in a pop-up
</button>
{% /html %}