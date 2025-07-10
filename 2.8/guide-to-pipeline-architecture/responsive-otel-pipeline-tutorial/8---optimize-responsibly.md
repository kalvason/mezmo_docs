---
type: page
title: 8 - Test the Responsive Pipelines
listed: true
slug: 8---optimize-responsibly
description: 
index_title: 8 - Test the Responsive Pipelines
hidden: 
keywords: 
tags: 
---

{% synced id="workshop-need-help" %}
{% /synced %}

## Why It Matters

Telemetry data is both fundamental and costly for any business.  While this data is invaluable for troubleshooting, monitoring and various other concerns, it is not always valuable at the same time.

Mezmo introduced [Responsive Pipelines](https://docs.mezmo.com/telemetry-pipelines/configure-responsive-pipelines) specifically to address the dynamic nature of telemetry data.  By allowing for extreme configurability, telemetry flows can be tuned for changing circumstances from incidents to deployments.

## 1 - Modify Responsive Test script

Using the State ID's for your Log, Metric and Trace pipelines modify [`switch_state.sh`](https://github.com/braxtonj/opentelemetry-demo/blob/main/switch_state.sh) with the proper credentials.

## 2 - Run Responsive Test Script

Now let's run the script with your desired state to initiate Mezmo Pipeline flow changes.  For instance, to flip to Incident mode you would run:

{% code %}
{% tab language="bash" %}
sh switch_state.sh incident
{% /tab %}
{% /code %}

## 3 - Evaluate Impact

Notice that when in `Normal` mode, data in your pipelines are sampled and rolled up ensuring the needed signals are captured while remaining cost conscious.  However, when in `Incident` or `Deployment` modes, data is grabbed at full fidelity.  You will also see this represented in the Mezmo Web App. 

### Normal Mode

{% image url="https://uploads.developerhub.io/prod/2KW7/1jl0ugjtknek6rrrl233ah2gtl32teowj9sdk28yq8k7trglsr6wezh0feh5y1hr.png" caption="Normal Mode" mode="responsive" height="1430" width="3042" %}
{% /image %}

### Incident Mode

{% image url="https://uploads.developerhub.io/prod/2KW7/71tfpfrsehwe1zr3rtpg9xl9zcsk6z0movm91ujouom9zyhp8x0i4ji11ewxf656.png" caption="Incident Mode" mode="responsive" height="1430" width="3042" %}
{% /image %}

Due to the flexibility of [Mezmo's API](https://docs.mezmo.com/pipeline-api), any pipeline can be integrated with just about any Incident Management or Deployment method, from PagerDuty to Github to Shell scripts.  To learn more, reach out to Mezmo at [support@mezmo.com](mailto:support@mezmo.com).