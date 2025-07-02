---
type: page
title: January 23th, 2020 - LogDNA Web Version 2.18.2
listed: true
slug: sd
description: 
index_title: January 23th, 2020 - LogDNA Web Version 2.18.2
hidden: 
keywords: 
tags: 
---




## Added
* Import/Export Screens - You can now import and export screens using the import/export feature found under Settings &gt; Organization &gt; Export Config / Import Config
* Added `_original_level` for the original log level received, and `level` continues to hold the parsed log level.

## Bugs
* Fixed an issue where parsed object fields are not searchable
* Fixed an issue with reserved fields were not being properly parsed with nested properties
* Make Logspout and Kubernetes log line level parsing more accurate
* Fixed a scrolling issue with extract fields.
* Fixed a bug not allowing non-team members to be added to alerts.
* Fixed a bug where certain users couldn't see the Export Lines feature.
* Fixed a bug where users would hit "Maximum Team Members Reached" in error.

## Changed
* Split up Import and Export pages, viewable at Settings &gt; Organization &gt; Export Config / Import Config

## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (now removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

