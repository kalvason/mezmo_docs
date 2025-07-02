---
type: page
title: Set Up Mezmo Edge in a Docker Container
listed: true
slug: set-up-mezmo-edge-in-a-docker-container
description: 
index_title: Set Up Mezmo Edge in a Docker Container
hidden: 
keywords: 
tags: 
---

## Getting Started

You can run Edge as a single Docker container within a suitable environment. In this deployment model, there is no default scaling other than the vertical scaling from the container resource allocation. You should be aware of this when planning your deployment resource allocation.

## Environment

You must have access to a Docker environment with sufficient privileges

### Set Environmental Variables

Set these default variables, including your Pipeline Service Key. 

{% callout type="info" title="Get a Service Key" %}
If you need a service key for your Edge instance, in your account go to **Settings** **&gt; Organization &gt; API keys** and find the Pipeline Service Key generation at the bottom of the page.
{% /callout %}

{% code %}
{% tab language="bash" %}
export EDGE_ID=<your name here>
export MEZMO_API_URI=https://api.mezmo.com/v3/pipeline/account/local-deploy
export MEZMO_PIPELINE_SERVICE_KEY='your_key_here'
{% /tab %}
{% /code %}

### Add Config Files

Add these two `.yaml`files to your working directory.

#### compose.yaml

{% code %}
{% tab language="yaml" %}
services:
  edge:
    image: 'mezmohq/vector:3.1.2'
    environment:
       MEZMO_LOCAL_DEPLOY_AUTH_TOKEN: ${MEZMO_PIPELINE_SERVICE_KEY}
      MEZMO_API_URI: ${MEZMO_API_URI}
      MEZMO_EDGE_ID: ${EDGE_ID}
       MEZMO_METRICS_ENDPOINT_URL: ${MEZMO_API_URI}/metric/usage?edge_id=${EDGE_ID}
       MEZMO_TASKS_FETCH_ENDPOINT_URL: ${MEZMO_API_URI}/tasks?edge_id=${EDGE_ID}
       MEZMO_TASKS_POST_ENDPOINT_URL: ${MEZMO_API_URI}/tasks/:task_id/results
       MEZMO_RESHAPE_MESSAGE: 1
    ports:
       - "8000-8010:8000-8010" # specify the port allocation range
    volumes:
       - ${PWD}/processor.yaml:/etc/vector/processor.yaml
       # change this to a host mount to test specific volumes for disk buffering
       - ${PWD}/tmp-data:/data/vector
     command: ["--config-dir", "/etc/vector"]
{% /tab %}
{% /code %}

#### processor.yaml

{% code %}
{% tab language="yaml" %}
provider:
  type: http
  url: ${MEZMO_API_URI}/config
  poll_interval_secs: 15
  request:
    headers:
      authorization: "Key ${MEZMO_LOCAL_DEPLOY_AUTH_KEY}"
    payload: "{\"edge_id\":\"${MEZMO_EDGE_ID}\",\"name\":\"edge\",\"namespace\":\"default\",\"ports\":[8000,8001,8002,8003,8004,8005,8006,8007,8008,8009,8010],\"replica\":\"0\",\"version\":\"edge-0.8.2\"}"
{% /tab %}
{% /code %}

### Run Docker Compose

{% code %}
{% tab language="bash" %}
docker compose up -d
{% /tab %}
{% /code %}

Start the Edge instance with this command:

{% code %}
{% tab language="bash" %}
docker ps
{% /tab %}
{% /code %}