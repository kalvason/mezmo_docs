---
type: page
title: April 22nd, 2020 - LogDNA Web Version 2.20.0
listed: true
slug: april-22nd-2020-logdna-web-version-2200
description: 
index_title: April 22nd, 2020 - LogDNA Web Version 2.20.0
hidden: 
keywords: 
tags: 
---




## Added
* Button to click to jump to the selected log line (ctrl/cmd + click)

## Enhancements
* Added a loading indicator when loading more lines while scrolling
* Improved the UI for handling no results within a restricted time range search.
* Support incomplete end dates/times ex. 'March 15 to 16'
* Added ability to copy raw line or displayed line depending if raw line is enabled.


## Bugs
* Fix flashing scrollbar UI on navigation item expand/collapse
* No longer show an error when a new search was conducted while a previous search was still in progress
* No longer show an error for the side histogram when on a free account
* Direct the user to the original URL link after logging in via SSO instead of a generic home page
* Support host names with a comma in them
* Search properly for queries with a comma in them
* Fix a bug to support displaying multi-line raw lines.
* Fix search loading bar to display below the filter bar
* Fix a bug to delete an alert in the manage alerts page
* Fix a bug where nested fields don't show up in alerts
* Fix a bug where alerts would not fire on views that contain ":" in the search


## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (now removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

