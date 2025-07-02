---
type: page
title: Mezmo Agent/Mezmo OTel Exporter
listed: true
slug: mezmo-agent-pipeline-source
description: 
index_title: Mezmo Agent/Mezmo OTel Exporter
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#description)

The Mezmo Agent Pipeline Source enables streaming of log data from the Mezmo Agent directly to your Pipeline.

## [Mezmo Agent Configuration](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#mezmo-agent-configuration)

You must configure your Agent to point to the pipeline data ingestion endpoint in order to use this source:

`pipeline.app.mezmo.com`.

This is not the same as the existing Mezmo ingestion API endpoint.

To use the Mezmo Agent as a source for Mezmo Pipelines, you must add your API key into the configuration of the Agent. You can find this by logging into the Mezmo Web App and navigating to **Settings &gt; Organization &gt; API Keys**.

You can find more information about configuring the Mezmo Agent in the topic [auto$](/docs/introducing-the-agent).

## [Mezmo OTel Exporter Configuration](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#mezmo-otel-exporter-configuration)

You can export your log data directly to Mezmo with the OpenTelemetry Exporter. If you are already using OpenTelemetry Collector, you can start sending log data by adding the mezmo exporter to your existing pipelines. If you are new to OTEL, you can use this quick start example to get you up and running.

### [Set Up OpenTelemetry Exporter](https://docs.mezmo.com/docs/mezmo-agent-pipeline-source#set-up-opentelemetry-exporter)

{% callout type="info" title="Log Data Only" %}
The Mezmo Exporter only supports capturing log data. **Metrics** and **Traces** from OTEL will not be captured.
{% /callout %}

1. Download the appropriate OTEL collector for your environment from [the OpenTelemetry website](https://github.com/open-telemetry).
2. Create a configuration file called `config.yaml` with these contents:

{% code %}
{% tab language="yaml" %}
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

4. Start the collector with this command: `--config=/path/to/config.yaml`
5. Create`.json` files in this directory.
6. As you add json lines to this file they will appear in the Log Viewer in Mezmo.

For complete information on setting up and configuring the OpenTelemetry Export for Mezmo log ingestion, check out [the GitHub repo for the mezmoexporter](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/exporter/mezmoexporter/README.md).

{% callout type="info" title="Default Hostname" %}
`otel`will be set at the default hostname for collector logs only if your logs don’t have a hostname set in the log metadata. You cannot set this metadata hostname in your collector configuration. Instead, recent changes to the collector configuration will enable the collector to recognize the hostname data from from incoming logs, and add that data to the internal OTEL representation of the log. The Mezmo OTEL Exporter will then attach the hostname data to the outgoing logs. For more information, see [the OTel Exporter changelog in GitHub](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/CHANGELOG.md).
{% /callout %}

{% callout type="info" title="Don't Forget the Ingestion Key!" %}
For `ingest_key`in the `config.yaml` file, enter your Mezmo Ingestion Key. You can find this by logging into [the Mezmo Web App](https://app.mezmo.com), and navigating to **Settings &gt; Organization &gt; API Keys**.
{% /callout %}

For complete information on setting up and configuring the OpenTelemetry Export for Mezmo log ingestion, check out [the GitHub repo for the mezmoexporter](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/exporter/mezmoexporter/README.md).