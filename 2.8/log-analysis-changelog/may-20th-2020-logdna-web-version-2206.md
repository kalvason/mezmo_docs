---
type: page
title: May 20th, 2020 - LogDNA Web Version 2.20.6
listed: true
slug: may-20th-2020-logdna-web-version-2206
description: 
index_title: May 20th, 2020 - LogDNA Web Version 2.20.6
hidden: 
keywords: 
tags: 
---



## Bugs
* Fixed a bug where the log viewer histogram time range query would be incorrect, leading to truncated histograms.
* Fixed a bug where custom fields took a day to appear to be available to be graphed on instead of the expected 15 minutes.
* Fixed a bug that stops redundant fetching of new lines when live tail is already enabled.
* Fixed a bug that resulted in empty archive files being uploaded for Azure Blob storage customers.
* Fixed a bug where the board name would not display while using the condensed side bar.
* Fixed a bug in the in-app NXLog documentation to properly display the NXLog port.

## Changes
* Updated in-app documentation for Kubernetes to install agent 2.1.

## Enhancements
* Added an error message when there's an issue with live tailing logs
* Added a toast when the user goes offline while in the web app

## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (now removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

