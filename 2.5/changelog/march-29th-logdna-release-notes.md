---
type: page
title: March 29th LogDNA Release Notes
listed: true
slug: march-29th-logdna-release-notes
description: 
index_title: March 29th LogDNA Release Notes
hidden: 
keywords: 
tags: 
---


## LogDNA Web Application, version 4.71.2

### New Features and Enhancements

- LogDNA now supports [two-factor authentication (2FA)](https://docs.logdna.com/docs/user-preferences) for users, adding more security to the log-in process. [LOG-8623]
- Enhanced functionality for copying objects from an expanded log line in the LogDNA Viewer :
- you can now copy an entire original JSON object from JSON-based log lines. [LOG-8814]
- the values shown in expanded log lines now provides a "copy to clipboard" action, as well as the ability to zoom in or out. [LOG-8424]
- Now an integer type field is searchable as a field in the Histogram breakdown of a board's graph. Previously only string values were searchable in the Histogram breakdown option. [LOG-8372]

### Fixed Issues

- This release of the LogDNA web application has improved contrast in line colors on charts, to increase visibility. [LOG-8282]
- We fixed an issue with searching for a specific time in UTC where the log viewer seems to search from the beginning of retention. [LOG-8880]
- We replaced with a correct version the NXLog configuration file referenced by our UI-based instructions. [LOG-8248]
- The Viewer Tools background color was modified to make the tools easier to read and more accessible. [LOG-9205]
- We fixed an issue with the search function for Slack/PagerDuty channel not working correctly. [LOG-9167]

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

## LogDNA APIs

There are no external-facing changes to our LogDNA APIs in this release.

