---
type: page
title: Mezmo January 2023 Release Notes
listed: true
slug: january-2023-release-notes
description: 
index_title: Mezmo January 2023 Release Notes
hidden: 
keywords: 
tags: 
---

Mezmo is pleased to announce the release of several new features for our log management, processing, and analysis platform.

## Webhook Alerts for Index Rate Alerting

You can now set up webhook alerts within the UI, API and Terraform Provider to alert you whenever your index rate thresholds are met. 

## Screens and Boards Enhancements

- Export Histograms as CSV and JSON
- Increased discoverability of Board Subplots
- Surface subplots with more than 10 fields
- Increase the max # of Board Subplots to 30
- Increase the max # of rows in Screens Table widget to 25
- Edit the name of Histogram Charts
- New Palette Chart Colors

## Log Data Size Enrichment

Every log line ingested has a new metadata field, `_mezmo_line_size`, that indicates the uncompressed size of that particular line.

## Agent 3.8 Beta

- Exclude/include logs from pods based on annotations and labels
- Collect image name and tag for containers as metadata for each log line
- FIX: Very frequent DNS requests made when requests to DNS service are rejected
- FIX: Advanced Glob and Regex patterns not recognized and causing files to be ignored

## Usage API v2

Customers can now query for usage by bytes as well as for a breakdown of the usage by apps, sources and tags.

## Downgrade Accounts Workflow (Self Service Customers Only)

We’ve updated the procedure for dealing with accounts with failed credit card payments. After a month of failed credit card payments, accounts will be switched to the free community plan with no stored ingestion.

## Account API Update (Contract Customers Only)

Enterprise Org customers can now query for their child accounts' service keys.