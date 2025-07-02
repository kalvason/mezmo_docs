---
type: page
title: Prometheus Remote Write
listed: true
slug: prometheus-remote-write-source
description: 
index_title: Prometheus Remote Write
hidden: 
keywords: 
tags: 
---


## Description

You can send your metrics to a Mezmo Pipeline to be received as Prometheus Remote Write data.

## Configuration

The Mezmo Prometheus Remote Write source provides a unique endpoint URL that uses **Bearer Token** authentication. You can obtain the unique endpoint and Bearer Token from the Mezmo pipeline app when you create a new Prometheus Remote Write source.

### Configuration Options

{% table %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| url | unique URL for your remote_write source | 
| bearer_token | token used in sending data to your remote_write source | 
{% /table %}

{% /table %}

### Prometheus Configuration File

To configure a Prometheus instance add a section like this to its configuration file:

{% code %}
{% tab language="yaml" %}
     - url: https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;
       bearer_token: &lt;YOUR_PIPELINE_INGEST_KEY&gt;
{% /tab %}
{% /code %}

### Kubernetes Operator

If you are running Prometheus within Kubernetes using the Kubernetes operator you can configure the instance with these commands, templating in the Bearer Token, the endpoint provided by the Mezmo Web App, and the Prometheus crd name:

{% code %}
{% tab language="bash" %}
kubectl -n monitoring create secret generic mz-prom-rw-token --from-literal=value=&lt;TOKEN FROM APP&gt;
{% /tab %}
{% /code %}

{% code %}
{% tab language="bash" %}
cat &lt;&lt;'EOF' | kubectl patch prometheus -n &lt;PROMETHEUS NAMESPACE&gt; &lt;YOUR PROMETHEUS CRD INSTANCE&gt; -f -
spec:
  remoteWrite:
  - authorization:
      credentials:
        key: value
        name: mz-prom-rw-token
    url: &lt;ENDPOINT FROM APP&gt;
EOF
{% /tab %}
{% /code %}