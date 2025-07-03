---
type: page
title: Mezmo Agent
listed: true
slug: mezmo-agent-source
description: 
index_title: Mezmo Agent
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#description)

The Mezmo Agent Pipeline Source enables streaming of log data from the Mezmo Agent directly to your Pipeline.

## [Mezmo Agent Configuration](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#mezmo-agent-configuration)

{% table widths="222,180" %}

{% table %}
| Environment Variable Name | Yaml Variable Name | Description | 
| ---- | ---- | ---- | 
| `MZ_ENDPOINT` | `http.endpoint` | Path of your Pipeline.  For all Pipelines this should be set to `/v1/<YOUR ROUTE ID>` | 
| `MZ_HOST` | `http.host` | The ingest endpoint for your Pipeline.  Should be a value similar to `pipeline.mezmo.com` | 
| `MZ_INGESTION_KEY` | `http.ingestion_key` | This is the access key to your Pipeline. | 
| `MZ_INGEST_BUFFER_SIZE` | `http.body_size` | Limit the body size per request in bytes (please configure to `1000000` or less) | 
{% /table %}

{% /table %}

### Migrating from Log Analysis

Please upgrade your Agent version to 3.9 or above before starting your migration to Pipeline ingestion. You may already have similar variables configured to point to your log analysis endpoint (prefixed with `LOGDNA_`). Just update these settings to the values in the table with values provided by your Pipeline setup. Please note the the `MZ_`prefix is only supported for Agent version 3.7+.

You can find more information about Agent settings in the [Agent GitHub repo](https://github.com/logdna/logdna-agent-v2/tree/master/docs#options).

For complete information on setting up and configuring the OpenTelemetry Export for Mezmo log ingestion, check out [the GitHub repo for the mezmoexporter](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/exporter/mezmoexporter/README.md).

## Installing via Helm

If your cluster is managed with Helm, you can also install the Mezmo Agent for Pipeline using Helm.  Utilizing the same information above, you can set these environment variables using the `extraEnv`  attribute.

{% callout type="info" title="Use Agent Key for &lt;YOUR_PIPELINE_INGEST_KEY&gt;" %}
In the YAML file example shown here, replace `<YOUR_PIPELINE_INGEST_KEY>` with the key you obtained when setting up the Agent source in your Pipeline. When using the environment variables shown in the Configuration section, this is also the same value you would set for `MZ_INGESTION_KEY`.
{% /callout %}

{% code %}
{% tab language="bash" %}
helm repo add logdna https://assets.logdna.com/charts
helm install --set 'logdna.key=&lt;YOUR_PIPELINE_INGEST_KEY&gt;,extraEnv[0].name=MZ_ENDPOINT,extraEnv[0].value=/v1/YOUR_PIPELINE_ID,extraEnv[1].name=MZ_HOST,extraEnv[1].value=pipeline.mezmo.com,extraEnv[2].name=MZ_INGEST_BUFFER_SIZE,extraEnv[2].value=1000000'  my-release logdna/agent
{% /tab %}
{% /code %}

Or using a `values.yaml`

{% code %}
{% tab language="yaml" %}
logdna:
key: &lt;YOUR_PIPELINE_INGEST_KEY&gt;
extraEnv:
- name: MZ_HOST
value: pipeline.mezmo.com
- name: MZ_INGEST_BUFFER_SIZE
value: 1000000
- name: MZ_ENDPOINT
value: /v1/&lt;YOUR ROUTE ID&gt;
{% /tab %}
{% /code %}

{% code %}
{% tab language="bash" %}
helm repo add logdna https://assets.logdna.com/charts
helm install -f ./values.yaml my-release logdna/agent
{% /tab %}
{% /code %}