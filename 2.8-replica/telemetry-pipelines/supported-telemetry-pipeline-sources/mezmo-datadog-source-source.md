---
type: page
title: Datadog Agent
listed: true
slug: mezmo-datadog-source-source
description: 
index_title: Datadog Agent
hidden: 
keywords: 
tags: 
---


{% callout type="info" title="Early Access Feature" %}
This feature is currently in early access mode. Please contact your Mezmo rep to gain direct access.
{% /callout %}

## Description

The [Datadog Agent](https://docs.datadoghq.com/agent/) is an open source agent that runs on a host to collect logs and metrics. This agent can be run locally per host, within Docker, or within Kubernetes. The `Datadog Agent Source` within Mezmo Pipeline is designed to receive data directly from the Agent via HTTPS. Mezmo can receive metrics individually, logs individually, or both simultaneously.

{% synced id="datadogflow" %}
{% /synced %}

## Requirements

The running agent version must be [ &gt;= 6.35 or &gt;= 7.35 ]

## Mezmo Pipeline Configuration

Adding a Datadog Agent source to a Pipeline is similar to adding a standard HTTP source. Add a source and choose **Datadog Agent**, optionally enter a **Title** and **Description**, then click `Save`.

Edit the node configuration:

Under `Access Key Management`

- Click the `Create new key` button
- Enter a `title`
- Choose the access key type as `User Defined`
- Enter your `Datadog API key`
- Click the `Create` button

Note the instructions with the overrides for `DD_LOGS_CONFIG_LOGS_DD_URL` and `DD_DD_URL`. These will be used directly in the Datadog Agent configuration.

Finish configuring the pipeline as desired and deploy.

### Datadog Agent Configuration

{% table widths="" %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| `DD_API_KEY` | The Datadog api key the agent is running with. | 
| `DD_DD_URL` | (optional) The custom Mezmo pipeline url to forward Datadog metrics to. | 
| `DD_LOGS_CONFIG_LOGS_DD_URL` | (optional) The custom Mezmo pipeline url to forward Datadog collected logs to. | 
| `DD_LOGS_ENABLED` | Set this configuration to true to allow the agent to collect logs. | 
{% /table %}

{% /table %}

## Examples

Datadog has provided detailed descriptions and various examples of agent configurations for the various systems:

- [host agent](https://docs.datadoghq.com/agent/logs/?tab=tailfiles)
- [docker](https://docs.datadoghq.com/containers/docker/log/?tab=containerinstallation)
- [kubernetes](https://docs.datadoghq.com/containers/kubernetes/log/?tab=operator)


#### Running the Datadog Agent via Docker:

Example pipeline publishing both logs and metrics to Mezmo:

{% code %}
{% tab language="bash" %}
docker run -d --name datadog-agent \
--cgroupns host \
--pid host \
-e DD_API_KEY=&lt;DATADOG_API_KEY&gt; \
-e DD_LOGS_ENABLED=true \
-e DD_LOGS_CONFIG_CONTAINER_COLLECT_ALL=true \
-e DD_LOGS_CONFIG_DOCKER_CONTAINER_USE_FILE=true \
-e DD_CONTAINER_EXCLUDE="name:datadog-agent" \
-e DD_DD_URL="https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;" \
-e DD_LOGS_CONFIG_LOGS_DD_URL="&lt;YOUR ROUTE ID&gt;.v1.pipeline.mezmo.com:443" \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v /var/lib/docker/containers:/var/lib/docker/containers:ro \
-v /opt/datadog-agent/run:/opt/datadog-agent/run:rw \
gcr.io/datadoghq/agent:latest
{% /tab %}
{% /code %}

Note that `DD_LOGS_CONFIG_LOGS_DD_URL` override does not contain `https`as the protocol is already assumed by the agent.

### Running the local datadog agent

[https://docs.datadoghq.com/agent/guide/agent-configuration-files/?tab=agentv6v7](https://docs.datadoghq.com/agent/guide/agent-configuration-files/?tab=agentv6v7)

Example pipeline publishing both logs and metrics to Mezmo:

{% code %}
{% tab language="yaml" %}
api_key: &lt;key&gt;
dd_url: https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;
logs_enabled: true
logs_config:
container_collect_all: true
logs_dd_url: &lt;YOUR ROUTE ID&gt;.v1.pipeline.mezmo.com:443
{% /tab %}
{% /code %}