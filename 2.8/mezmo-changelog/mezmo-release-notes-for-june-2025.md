---
type: page
title: Mezmo Release Notes for June 2025
listed: true
slug: mezmo-release-notes-for-june-2025
description: 
index_title: Mezmo Release Notes for June 2025
hidden: 
keywords: 
tags: 
---


## Features

### Datadog Cost Reduction Flow

When creating a new Pipeline, you now have the option to use [Mezmo Flow](/telemetry-pipelines/about-mezmo-flow) flow to build a specialized pipeline to reduce your Datadog costs. Check out the [auto$](/telemetry-pipelines/mezmo-datadog-source-source) topic for more information.

## Bug Fixes

**LOG-20150** [kafka-bridge] does not scale up well

**LOG-21907** [pipeline-service] handle migrations when table exists but no migration happened

**LOG-21910** Update /v3/pipelines PUT/POST endpoints to not allow extra fields

**LOG-21925** The color filled data rows have the color shifting with pages

**OG-20324** Times in pipeline restoration UI in the wrong order

**LOG-20409** Exported lines ingested with syslog missing keys for null/undefined field, with quickwit

**LOG-21721** "map fields" processor on a pure string message replaces the message

**LOG-21739** [vector] aggregate_distributed lag under high throughput

**LOG-21935** Fix alert expectation in revision get spec

**LOG-21714** [vector] Aggregate (aggregate_v2) processor "stuck" when consumer lag builds

**LOG-21789** Incorrect log lines showing up in different views

**LOG-21790** Admin users in LA Only accounts can still see the Pipeline Restoration link

**LOG-21839** Investigate and fix 'TypeError: next is not a function' in billing endpoints

**LOG-21851** Investigate and resolve HTTP 400 error when posting absence alert cache

**LOG-21889** [otel] tags/attributes are not being sent in the data payloads to otel