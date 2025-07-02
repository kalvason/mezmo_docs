---
type: page
title: Oct 14th, 2020 - LogDNA Web Version 4.2.6
listed: true
slug: oct-14th-2020-logdna-web-version-426
description: 
index_title: Oct 14th, 2020 - LogDNA Web Version 4.2.6
hidden: 
keywords: 
tags: 
---




## Bugs
* Fixed a bug where the "Manage Team" link within the team join notification email would lead to the incorrect URL
* Fixed a bug where verification email codes would not be successfully emailed to invited team members
* Fixed a bug where Viewer Tools panel would be obscured by the Timeline panel
* Fixed a bug where occasionally elements in the UI would be spaced incorrectly
* Fixed a bug where live tail in CLI would not load correctly
* Fixed a bug where Widget labels would occasionally disappear when window is resized
* Fixed a bug where there would be occasional repeat values in the Y axis of Graphs
* Fixed a bug where long app names would occasionally cause the log line to render off screen

## Enhancements
* Added tooltips to show the full name of an app on hover in the "App" filter.
* Added help text to explain why certain authentication options can not be disabled by the current user.
* Improved loading speed of Timeline
* Added "Apply" button to filters
* Improved in-app code library installation instructions
* Improved monthly usage graph to better visualize and gauge account usage
* Improved retry and error handling when part of a search request fails to complete

## Added
* Added support for `@logdna/logger` to be run in the browser

## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (recently removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

