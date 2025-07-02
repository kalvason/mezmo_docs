---
type: page
title: Mezmo Release Notes for May 2025
listed: true
slug: mezmo-release-notes-for-may-2025
description: 
index_title: Mezmo Release Notes for May 2025
hidden: 
keywords: 
tags: 
---


Mezmo is pleased to announce new features and updates for the Mezmo Platform.

## Features

### Pipeline Sources and Destinations for Checkly

With the new [Source](https://docs.mezmo.com/telemetry-pipelines/checkly) and[ Destination ](https://docs.mezmo.com/telemetry-pipelines/checkly-destination)components for [Checkly](https://www.checklyhq.com/), you can both receive and send telemetry traces based on the OpenTelemetry standard for you Checkly instances. [Check out this blog post](https://www.checklyhq.com/blog/streamlining-telemetry-mezmo/) for more information about using Checkly with a Mezmo Telemetry Pipeline.

### Bug Fixes

**LOG-17714** pipeline "paused" and "internet connection found, refresh" toasts overlap

**LOG-21622** [pipeline-account-manager-job] don't notify disabled accounts if disabling account fails

**LOG-21717** [vector] aggregate_distributed fails to flush with ~12,000+ expired windows

**LOG-21778** Log Metrics missing from profiles after running Log Classification node always

**LOG-21793** Intermittent CI failures due to flakey revert pipeline and withComponent tests

**LOG-21819** [surge-detection-job] sqrt of a negative error in getHistoricalHourUsage()

**LOG-21704** expanded "field summary" items have a huge amount of bottom whitespace

**LOG-21733** [pipeline-ui] Copy fields paths for arrays is incorrect