---
type: page
title: Sumo Logic Logs
listed: true
slug: sumo-logic-logs-destination
description: 
index_title: Sumo Logic Logs
hidden: 
keywords: 
tags: 
---

## Description

This destination lets you send logs to your Sumo Logic instance.

## Configuration

The destination can be configured according to these options.

{% table %}
| Option | Description | 
| ---- | ---- | 
| Collector Endpoint | The Sumo Logic collector URL that receives the logs | 
| Compression | Compression strategy to use | 
| Category | Category to use when publishing to Sumo Logic (defaults to `mezmo_default_category` | 
{% /table %}