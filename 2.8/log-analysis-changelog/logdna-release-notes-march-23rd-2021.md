---
type: page
title: LogDNA Web Application, version 4.69.3
listed: true
slug: logdna-release-notes-march-23rd-2021
description: 
index_title: LogDNA Web Application, version 4.69.3
hidden: 
keywords: 
tags: 
---

## LogDNA Web Application, version 4.69.3

### New Features and Enhancements

- LogDNA now integrates with Sysdig and allows you to configure alerts, based on log lines ingested by LogDNA, that trigger new events in your Sysdig instance. For more details refer to our [documentation](https://docs.logdna.com/docs/sysdig-alert-integration). [LOG-9004, LOG-9101]
- Our [Custom Log Line Templates](/docs/format-log-lines-with--custom-line-templates) now return the same search results for a field name that is preceded by an underscore (`_field`) and one that is not.  This change was made to be consistent with how our regular search, outside of line templates, supports both underscore and non-underscore versions. [LOG-7171]
- Previously, if a view that you were looking at in the web application UI was modified by an API event, and you refreshed the view in the web application UI, the changes made by the API were not displayed even after refreshing. To refresh the view, you needed to navigate to a different View and then back to the original one. Now, in order to refresh and see the current configuration of the view, you can click the name of the view on the left-hand navigation pane, and the view will reset with the view’s latest filter/search properties. [LOG-8115]

### Fixed Issues

- We fixed an issue where if you use the Filter option in the menu bar of the web application to create a new group, live tail stoped functioning when only the new group was selected. [LOG-8838]

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

##LogDNA APIs

There are no external-facing changes to our LogDNA APIs in this release.