---
type: page
title: 1 - Introduction
listed: true
slug: 1--introduction
description: 
index_title: 1 - Introduction
hidden: 
keywords: 
tags: 
---

{% synced id="workshop-need-help" %}
{% /synced %}

## Perequisites

- A Mezmo account, you can [sign up for a trial here](https://www.mezmo.com/sign-up-mezmo-platform).
- [Docker](https://www.docker.com/get-started/) 

## Overview

In this workshop, we will be exploring telemetry data produced with the [OpenTelemetry Demo](https://github.com/braxtonj/opentelemetry-demo) while optimizing it for both MTTR and cost.

To accomplish this we will:

1. Create a OpenTelemetry Log, Metric, and Trace [Shared Source](https://docs.mezmo.com/telemetry-pipelines/shared-sources) in Mezmo.
2. [Configure OpenTelemetry collector](https://github.com/braxtonj/opentelemetry-demo/mezmo-otel-config-extras.yml) with Mezmo Shared Source credentials.
3. Explore the OpenTelemetry Logs via [Data Profiling](https://docs.mezmo.com/telemetry-pipelines/data-profiling)
4. Send log data to [Mezmo Log Analysis](https://docs.mezmo.com/docs)
5. [Aggregate](https://docs.mezmo.com/telemetry-pipelines/reduce-processor) specific log patterns
6. [Parse](https://docs.mezmo.com/telemetry-pipelines/parse-sequentially-processor) custom Apache data
7. [Aggregate OpenTelemetry Metrics](https://docs.mezmo.com/telemetry-pipelines/aggregate-processor) to lower fidelity
8. [Sample OpenTelemetry Traces](https://docs.mezmo.com/telemetry-pipelines/sample-processor)
9. Configure Pipelines to be [Responsive](https://docs.mezmo.com/telemetry-pipelines/configure-responsive-pipelines) (ie, capture full fidelity when in an incident or deployment state)

## Final Product

In the end you are going to build four Pipelines that look like these

- Log Profiling Pipeline

{% image url="https://uploads.developerhub.io/prod/2KW7/g96or2pxtsdxpgc45yft3j0xhrwlatg94c4pbkvw5xihtswcv5wgsavbuaffv6os.png" caption="Final Pipeline: Log Exploration" mode="responsive" height="1342" width="3330" %}
{% /image %}

- Log Handler Pipeline

{% image url="https://uploads.developerhub.io/prod/2KW7/cs3p6z7byoiz26szyfpi0tus3y98un7vtfmvnomu8ekiol0rddevhnpcw6iyuack.png" caption="Final Pipeline: Log Handler" mode="responsive" height="1000" width="3380" %}
{% /image %}

- Metric Handler Pipeline

{% image url="https://uploads.developerhub.io/prod/2KW7/1hr2day4vwx8w6m5977gkvy69q84gkgenqcop679zef4c340ysg0gddibpds66sf.png" caption="Final Pipeline: Metric Handler" mode="responsive" height="1150" width="3330" %}
{% /image %}

- Trace Handler Pipeline

{% image url="https://uploads.developerhub.io/prod/2KW7/i7jvfiyk5ps0x8horxotawsrwu2ia7rtiqe321pe0y4tuoz0i2zj9zk35c2hmaa2.png" caption="Final Pipeline: Trace Handler" mode="responsive" height="1462" width="3272" %}
{% /image %}

These pipelines will optimize your OpenTelemetry data by aggregating, parsing, and configuring data flow responsively. By allowing for easy, granular control you can make sure the right data winds up where it belongs.

The end result is a system that provides the insight needed, at the fidelity when it's needed, leading to an order of magnitude in savings.