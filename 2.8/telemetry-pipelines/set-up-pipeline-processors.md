---
type: page
title: Set Up Pipeline Processors
listed: true
slug: set-up-pipeline-processors
description: 
index_title: Set Up Pipeline Processors
hidden: 
keywords: 
tags: 
---


One of the most important functions of a telemetry pipeline is the ability to process log data to reduce its size, re-format and standardize it, or extract information from it for use in analytical operations. Mezmo Telemetry Pipelines include processors for an extensive set of use cases, that can be used independently for basic processing, or chained together for more complex operations. In this section you'll find a complete listing of Mezmo Pipeline Processors, including their common use cases and configuration.

1. Log into [the Mezmo Web App](https://app.mezmo.com/).
2. In the left-hand menu, click **Pipelines**. This will open the **Edit Pipeline** interface.
3. In the left-hand navigation, click **+ New Pipeline**.
4. Enter a name for the Pipeline, then click **Save**.
5. [Set up your Pipeline Sources](/telemetry-pipelines/set-up-pipeline-processors) and [Pipeline Destinations](/telemetry-pipelines/set-up-pipeline-destinations).
6. After you connect the Source and Destination, click the connector and the **Insert Node** dialog will open.
7. Select **Insert Node** and choose the Processor you want to apply to that Pipeline segment.

The topic [auto$](/telemetry-pipelines/supported-processors) provides a full list of available sources and their configuration instructions.

## Processor Module Tutorials

These tutorials provide an overview of typical Processor configurations for specific use cases. They include a schematic of the "Pipette" and configuration instructions for each module, an interactive demo, and step-by-step instructions for how to create your own version using [auto$](/telemetry-pipelines/demo-logs-source) and a [auto$](/telemetry-pipelines/blackhole-destination) Destination, and then connecting your own data sources and destinations.

- [auto$](/practioner-guide-data-optimization/pipeline-example--convert-200-events-to-metrics)
- [auto$](/practioner-guide-data-optimization/pipeline-module--route)
- [auto$](/practioner-guide-data-optimization/pipeline-module--security-and-compliance)

## Video Overview

{% video videoId="799543770" provider="vimeo" %}
{% /video %}