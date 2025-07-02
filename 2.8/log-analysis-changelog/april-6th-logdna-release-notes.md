---
type: page
title: April 6th, 2021 - LogDNA Release Notes
listed: true
slug: april-6th-logdna-release-notes
description: 
index_title: April 6th, 2021 - LogDNA Release Notes
hidden: 
keywords: 
tags: 
---



## LogDNA Web Application, version 4.79.3

### New Features and Enhancements

* LogDNA is pleased to announce enhancements for the Timeline graph in the web application UI, including the ability to zoom in to a selected time frame, examine those specific log lines for patterns or anomalies, and then either scope in further or "zoom out" to select a wider, contiguous time frame. Read more about this feature in our [documentation](https://docs.logdna.com/docs/working-with-the-timeline-visualization). [LOG-7851, LOG-9287]
* Users can now modify the height of log lines displayed in the LogDNA Viewer. Go to **User Preferences -&gt; Viewer Style** and use the slider to increase or decrease the display size of the log lines.

### Changes

* Archiving logs now implements **hourly archiving** instead of daily archiving. Learn more in our [documentation](https://docs.logdna.com/docs/archiving). [LOG-9037]
* Storing and showing raw log lines is now only available to Admins and Owners of an organization. [LOG-6864]

### Fixed Issues

* We fixed an issue where incorrect values were returned when creating a Table in Screens that was aggregated by multiple reserved fields. [LOG-9240]
* Implemented proper spacing for the checkboxes on the Alert modals.
* Removed reference to CentOS 6 in our application-based documentation. [LOG-9285]

## LogDNA Agent

For the most recent release information about the LogDNA Agent, refer to [agent-specific Release Notes](https://docs.logdna.com/changelog).

## LogDNA Integrations

There are no external-facing changes to our LogDNA integrations in this release.

##LogDNA APIs

There are no external-facing changes to our public LogDNA APIs in this release.

