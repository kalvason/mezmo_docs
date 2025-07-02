---
type: page
title: April 21st, 2021 - LogDNA Release Notes
listed: true
slug: april-21st-2021-logdna-release-notes
description: 
index_title: April 21st, 2021 - LogDNA Release Notes
hidden: 
keywords: 
tags: 
---




## LogDNA Web Application, version 4.90.9

### New Features and Enhancements
LogDNA is pleased to announce the following highlight of this release:
* NGINX Ingress Controller for Kubernetes Template, with pre-configured Views, Boards and Screens that you can customize and then configure alerts on 500's, graphs of response codes sorted by upstream service name, and more. The NGINX Ingress Controller is the latest in a set of LogDNA Templates. For more information, refer to our documentation about [using LogDNA Templates](https://docs.logdna.com/docs/using-templates).

## Changes
* We improved the error message that is returned when users search for logs outside of the retention period. [LOG-8867]

### Fixed Issues
* The threshold checkboxes for threshold percentages (25/50/75/100%) on Usage Quotas could not be checked or unchecked. [LOG-9467]
* Livetail stopped displaying when you selected either an **App** or **Source** filter that contained special symbols in the query string. [LOG-9112].


## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

## LogDNA APIs

This release includes the Export API, version 2.  This new version enables you to programmatically retrieve multiple batches of log files, using the `pagination_id` parameter to request subsequent sets of lines. Learn more about the new endpoint in our documentation [About the Export API](https://docs.logdna.com/reference?showHidden=44b66#about-the-export-api) and the [API v2 reference page](https://docs.logdna.com/reference?showHidden=44b66#export-v2).

