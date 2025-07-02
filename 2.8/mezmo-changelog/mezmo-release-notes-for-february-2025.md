---
type: page
title: Mezmo Release Notes for February 2025
listed: true
slug: mezmo-release-notes-for-february-2025
description: 
index_title: Mezmo Release Notes for February 2025
hidden: 
keywords: 
tags: 
---


Mezmo is pleased to announce new features and updates for the Mezmo Platform.

## Features


#### Data Profile Field Summaries

Field summaries provide the analysis of telemetry data from the perspective of field values. The **Field Summaries** section of the Data Profile  provides a tabular view of all the Fields discovered from the events that are streaming through a pipeline during a Data Profile analysis of your source data. For more information, check out [the Field Summaries section of the Data Profile topic](https://docs.mezmo.com/telemetry-pipelines/data-profiling#field-summaries)  in our documentation.

## Bug Fixes

**LOG-21330** DD agent source does not ingest metrics with new agent v7.62.0

**LOG-21393** [pipeline-service] Only blackhole unconnected leaf nodes from a transform group

**LOG-21400** [pipeline-assignment-loop] Legacy flag is not passed to Kong Admin API

**LOG-18694** Exported pipelines should include the host in the provider block if it's not the default

**LOG-20897** LogDNA Agent K8s panic when no /dev/null file exists

**LOG-21331** Redirect all old trial flows to /onboarding/lvr

**LOG-21351** [pipeline-ui] Aggregate processor only show change operators

**LOG-21366** Setting child org as default is not working

**LOG-21377** [kong-gateway] Jenkins is broken - APP_VERSION is null in main branch

**LOG-21390** [kong-gateway] DataDog handler proxy non decoded payload to a target endpoint

**LOG-21247** [field-summarization-job] don't double count size for integer type fields

**LOG-21350** [vector] config provider revalidates all transforms in the topology in some cases

**LOG-21352** [vector] perf with large pipeline topology created from LVR

**LOG-21252** Data Profiler: No classification data section shows up for a quick second

**LOG-21280** Histogram/Donut breakdown under Boards can't distribute on a field with "/" character

**LOG-21311** No classification data action button is not working

**LOG-21320** [pipeline-ui] Migrate exclusion rules issues

**LOG-21322** [pipeline-service] field summary aggregation node doesn't have persistence configured