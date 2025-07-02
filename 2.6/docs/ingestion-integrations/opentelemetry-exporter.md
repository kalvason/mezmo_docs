---
type: page
title: OpenTelemetry Exporter
listed: true
slug: opentelemetry-exporter
description: The OTEL Mezmo exporter provides export capabilities to your OpenTelemetry pipelines
index_title: OpenTelemetry Exporter
hidden: 
keywords: 
tags: 
---

You are now able to export your log data directly to Mezmo. If you are already using OpenTelemetry Collector, you can start sending log data by adding the mezmo exporter to your existing pipelines.  If you are new to OTEL, we’ve provided a quick start sample to get you up and running.

{% callout type="info" title="LogData Only" %}
The Mezmo Exporter only supports capturing log data.  **Metrics** and **Traces** from OTEL will not be captured.
{% /callout %}

### Set Up OpenTelemetry Exporter

1. Download the appropriate OTEL collector for your environment from [the OpenTelemetry website](https://opentelemetry.io/docs/collector/getting-started/)
2. Create a configuration file called `config.yaml` with these contents:

{% code %}
{% tab language="yaml" title="config.yaml" %}
receivers:
 filelog:
   include: [ ./*.json ]
   operators:   
     - type: json_parser
exporters:
  mezmo:
    ingest_url: "https://logs.mezmo.com/otel/ingest/rest"
    ingest_key: "<your ingestion key>"
service:
 pipelines:
   logs:
     receivers: [ filelog ]
     exporters: [ mezmo ]
{% /tab %}
{% /code %}

3. Start the collector with this command:

{% code %}
{% tab language="bash" %}
--config=/path/to/config.yaml
{% /tab %}
{% /code %}

4. Create `.json` files in this directory.
5. As you add json lines to this file they will appear in the Log Viewer in Mezmo.

For complete information on setting up and configuring the OpenTelemetry Export for Mezmo log ingestion, check out [the GitHub repo for the mezmoexporter](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/exporter/mezmoexporter/README.md).

{% callout type="info" title="Default Hostname for Collector Logs" %}
`otel` will be set at the default hostname for collector logs only if your logs don’t have a hostname set in the log metadata. You cannot set this metadata hostname in your collector configuration. Instead, recent changes to the collector configuration will enable the collector to recognize the hostname data from from incoming logs, and add that data to the internal OTEL representation of the log. The Mezmo OTEL Exporter will then attach the hostname data to the outgoing logs. For more information, see [the OTel Exporter changelog in GitHub](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/CHANGELOG.md).
{% /callout %}