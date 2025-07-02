---
type: page
title: Mezmo Release Notes for April 2025
listed: true
slug: mezmo-release-notes-for-april-2025
description: 
index_title: Mezmo Release Notes for April 2025
hidden: 
keywords: 
tags: 
---

Mezmo is pleased to announce updates for the Mezmo Platform.

## Bug Fixes

**LOG-21530** [ingestion-service] only override __metadata from pipeline route schema, throw out other values

**LOG-21569** Fix issues caused by pipeline_id addition to classification nodes

**LOG-21585** [pipeline-service] incorrect field summary max values env var name in deployment yaml

**LOG-21143** [vector] polling state variables from postgres doesn't limit query to only elements in the current partition

**LOG-21495** [pipeline-service] Deploying a pipeline with an empty processor group

**LOG-21576** Suggestion: Tap: always show the 'show data envelope' toggle

**LOG-21608** Fix with components endpoint for datadog agent source

**LOG-21635** Restrict LVR internally generated titles

**LOG-20982** [access keys] cannot deploy pipeline

**LOG-21333** going to a nodes profile via context link doesn't scroll to it

**LOG-21653** [vector] aggregate_distributed incorrect error message for invalid metric

**LOG-21662** "data profiler processor" filter drop down in profiler list has duplicates

**LOG-21667** [pipeline-service] Field Summary min/max/avg should be null for integer enum values

**LOG-21679** [pipeline-ui] Json viewer arrays

**LOG-21470** Pipeline Node Alerts aren't restored when reverting pipeline

**LOG-21548** Timestamp not restored correctly in pipeline -&gt; pipeline restoration flow

**LOG-21688** [vector] aggregate - adjust output event after testing

**LOG-21689** [vector] Mezmo env var handling is noisy, should explicitly handle empty strings as unset

**LOG-21692** Field Summary foot page numbers are not showing up when json log fields are more than 5

**LOG-21695** LVR Demo now utilizing app and host correctly

**LOG-21701** [pipeline-ui] data profiler should not allow clone

**LOG-21718** [pipeline-ui] Hide new pipeline flow for edge