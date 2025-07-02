---
type: page
title: Mezmo Release Notes for March 2025
listed: true
slug: mezmo-release-notes-for-march-2025
description: 
index_title: Mezmo Release Notes for March 2025
hidden: 
keywords: 
tags: 
---


Mezmo is pleased to announce new features and updates for the Mezmo Platform.

## Features

### Trace Sampling Processsor (Experimental)

With the Trace Sampling Processor, you can sample both head and trail traces at a specified  rate using the Trace ID as the unique identifier. If a trace is rate selected, all spans of the trace are output. You can find more information in [the Trace Sampling Processor topic in our documentation](https://docs.mezmo.com/telemetry-pipelines/trace-sampling-processor).

## Bug Fixes

**LOG-21064** Pipeline: Otel Dest introduces extra quotations, no annotations and no custom metadata

**LOG-21405** [tap] tail-based-sampling: no timestamp displayed

**LOG-21419** Discrepancy in total egress

**LOG-21289** Lines sent from syslog using RFC3164 not being handled correctly with Ingestion Router (incorrect timestamps, Live Tail and Alerting may be affected, will see `UNKNOWN_SYSLOG_APP` error)

**LOG-21423** Change/Threshold Alert selection does not update available operators

**LOG-21482** [pipeline-service] `inputs`  surge detection column added to wrong migration file

**LOG-21480** [pipeline-service] Field Summary not null constraint violation on insert

**LOG-21489** [pipeline-service/vector] Revisit sink buffer config and behavior with acks disabled

**LOG-21492** Fix Datadog event type header for logs and intake

**LOG-21414** `getStateVariable` returns null in Processor Groups

**LOG-21513** Sync Pipeline and LA trial lengths (30 days)

**LOG-21572** [pipeline-usage-alerts-job] refresh correct aggregate in test code