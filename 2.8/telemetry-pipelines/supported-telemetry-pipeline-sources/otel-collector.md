---
type: page
title: OpenTelemetry Collector
listed: true
slug: otel-collector
description: 
index_title: OpenTelemetry Collector
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#description)

You can export your log data directly to Mezmo with the OpenTelemetry Exporter. If you are already using OpenTelemetry Collector, you can start sending log data by adding the Mezmo Exporter to your existing Pipelines. If you are new to OTEL, you can use this quick start example to get you up and running.

### Example [OpenTelemetry Exporte](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#set-up-opentelemetry-exporter)r Setup

1. Download the appropriate OTEL collector for your environment from [the OpenTelemetry website](https://github.com/open-telemetry).
2. Create a new pipeline in Mezmo.
3. Add an [auto$](/telemetry-pipelines/open-telemetry-logs-source) Source node.  Note the Pipeline URL and access key.
4. Add an [auto$](/telemetry-pipelines/open-telemetry-metrics-source) Source node.  Note the Pipeline URL and access key.
5. Add an [auto$](/telemetry-pipelines/open-telemetry-traces-source) Source node.  Note the Pipeline URL and access key.
6. Create a configuration file `config.yaml` with these contents:

{% code %}
{% tab language="yaml" title="Pipeline YAML Configuration" %}
receivers:
  filelog: #This will collect new lines from log files in /var/log
    include: [/var/log/*.log] 
  hostmetrics: #This will collect metrics about the host on which the collector is running.
    scrapers:
      cpu:
      disk:
      filesystem:
      load:
      memory:
  jaeger: #This will expose an endpoint where you can send traces
    protocols:
      grpc:
        endpoint: "0.0.0.0:14250"
exporters:
  otlphttp/logs:
    endpoint: "<endpoint from Logs node>"
    headers:
      Authorization: "<access key from Logs node>"
  otlphttp/metrics:
    endpoint: "<endpoint from Metrics node>"
    headers:
      Authorization: "<access key from Metrics node>"
  otlphttp/traces:
    endpoint: "<endpoint from Traces node>"
    headers:
      Authorization: "<access key from Traces node>"
        
processors:
  batch:
  
service:
  pipelines:
    logs:
      receivers: [ filelog ]
      exporters: [ otlphttp/logs ]
    traces:
      receivers: [jaeger]
      processors: [batch]
      exporters: [otlphttp/traces]
    metrics:
      receivers: [hostmetrics]
      processors: [batch]
      exporters: [otlphttp/metrics]
{% /tab %}
{% /code %}

{% callout type="warning" title="Must Match the OpenTelemetry Metrics / Logs / Traces URL" %}
The endpoints in the exporters config must exactly match the URL provided by the OpenTelemetry Metrics / Logs / Traces sources, You don't need to specify the `/v1/metrics` `/v1/logs` `/v1/traces` paths, which will otherwise be ignored by the Sources.
{% /callout %}

4. Start the Collector with this command: `./otelcol-contrib --config /path/to/config.yaml`
5. The Collector will start sending logs, metrics and traces to your Pipeline.

{% callout type="info" title="This is an example setup" %}
For complete information on setting up and configuring the OpenTelemetry Collector, visit [https://opentelemetry.io/docs/collector/configuration](https://opentelemetry.io/docs/collector/configuration)
{% /callout %}

## Installing the Collector via a Helm Chart

You can install the OpenTelemetry collector directly in a Kubernetes cluster using a Helm chart.

If you don't have the OpenTelemetry repo added to your Helm list, you must add it first.

{% code %}
{% tab language="bash" %}
helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
{% /tab %}
{% /code %}

Update your repos once you've added the OpenTelemetry repo.

{% code %}
{% tab language="bash" %}
helm repo update
{% /tab %}
{% /code %}

Then you can install the chart to deploy the Collector. The example shown here installs as a single global endpoint for all data with a Splunk HEC format as indicated in the provided `.yaml`configuration. You may also provide a configuration of your own like the one above. 

To utilize this chart, create a Splunk HEC Source, and note the Endpoint and Token. As shown in this command,  replace `<YOUR PIPELINE INGEST ID HERE>`  with the ID portion of endpoint (the part that follows `/v1/` ).  Replace `<YOUR TOKEN HERE>`  with your provisioned token.

{% code %}
{% tab language="bash" %}
helm upgrade -i --create-namespace -n mezmo \
  mezmo-otel-collector open-telemetry/opentelemetry-collector \
  --values https://repo.mezmo.com/otel-collector/values.yaml \
  --set global.mezmo.endpoint="<YOUR ROUTE ID>" \
  --set global.mezmo.token="<YOUR TOKEN HERE>"
  --set image.repository="otel/opentelemetry-collector-contrib"
{% /tab %}
{% /code %}