---
type: page
title: Primary Ingestion Pipeline
listed: true
slug: the-log-analysis-source-data-pipeline
description: 
index_title: Primary Ingestion Pipeline
hidden: 
keywords: 
tags: 
---


In November of 2024, Mezmo Log Analysis customers were given access to a Pipeline designed specifically to provide them with an optimized log data management experience. This topic provides an overview of the new features available to customers through this Pipeline, as well as an overview of the Processors in this Pipeline and their configuration.

## Access the Pipeline

1. Log in to the Mezmo Web App.
2. Click the Pipeline icon at the top of the left navigation column.

{% callout type="error" title="Do Not Edit the Pipeline" %}
Do not edit the Pipeline without consulting Mezmo Technical Services.
{% /callout %}

## Pipeline Architecture

The Primary Ingestion Pipeline processes data in four steps, with each step designed to optimize your data for use with Mezmo Log Management.

{% image url="https://uploads.developerhub.io/prod/2KW7/d8jizv5xta6tdgr3d1z7zuwztw49l7ii3pmrxksl8lbtprpcvdqsodmimwq0ibx6.png" caption="_Schematic of the LASD Pipeline showing 1) the Mezmo Log Analysis Source 2) the Route Processor for Kubernetes Enrichment 3) the Drop Fields Processor 4) the Route Processor for Bad LInes 5) the Mezmo Log Analysis Destination 6)the Blackhole Destination_" mode="responsive" height="959" width="3262" %}
{% /image %}

{% table widths="" %}

{% table %}
| Component | Description | Configuration | 
| ---- | ---- | ---- | 
| 1. Mezmo Log Analysis Data Source |  |  | 
| 2. Route Processor | The [auto$](/telemetry-pipelines/route-processor) uses conditional statements to identify Kubernetes enrichment metrics, app/file metadata, and other relevant data for further processing, while unmatched data is sent directly to Log Analysis. | {% inline-image url="https:\\/\\/uploads.developerhub.io\\/prod\\/2KW7\\/tyh04lxdsigtonmi55hovtroclow1yq9ffcj2q9bny06o3eoq01ikhh252ygaznt.png" width="939" mode="w100" /%} | 
| 3. Remove Fields Processor | The [auto$](/telemetry-pipelines/drop-fields-processor) drops the .app field when a file is also present. | {% inline-image url="https:\\/\\/uploads.developerhub.io\\/prod\\/2KW7\\/fstjxllfw58f071eqvkcysxefr3khm30gqseewho45foufyt0qs3xx2x8chlm5rw.png" width="946" mode="w100" /%} | 
| 4. Route Processor | The [auto$](/telemetry-pipelines/route-processor) routes empty fields to a [auto$](/telemetry-pipelines/blackhole-destination) Destination, where they are dropped. | {% inline-image url="https:\\/\\/uploads.developerhub.io\\/prod\\/2KW7\\/fmd2o3bdhah36vvt3dz431n635n9swu14c0jwvzkwgk8ibxwcxjoqhajobsqvjqe.png" width="892" mode="w100" /%} | 
| 5. Log Analysis Destination | The processed telemetry data is sent to Mezmo Log Analysis. | {% inline-image url="https:\\/\\/uploads.developerhub.io\\/prod\\/2KW7\\/mfqjapuzyz0otmq3l8uhg96a2uc2yuk8gqksiveq8a12donygjwj5l5cjqre5f5s.png" width="887" mode="w100" /%} | 
| 6. Blackhole Destination | The [auto$](/telemetry-pipelines/blackhole-destination) Destination drops all data sent to it. |  | 
{% /table %}

{% /table %}

Learn More About Mezmo Telemetry Pipelines

Check out these links to learn more about Mezmo Telemetry Pipelines, and how you can optimize your telemetry data to reduce costs, gain insights, and quickly respond to anomalies and incidents.

- [auto$](/telemetry-pipelines/getting-started-with-mezmo-telemetry-pipeline)
- [auto$](/telemetry-pipelines/about-mezmo-flow)
- [auto$](/telemetry-pipelines/supported-processors)
- [auto$](/telemetry-pipelines/in-stream-alerts)
- [auto$](/telemetry-pipelines/configure-responsive-pipelines)