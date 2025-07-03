---
type: page
title: Aug 26th, 2020 - LogDNA Web Version 3.5.6
listed: true
slug: aug-26th-2020-logdna-web-version-356
description: 
index_title: Aug 26th, 2020 - LogDNA Web Version 3.5.6
hidden: 
keywords: 
tags: 
---




## Bugs
* Fixed a bug where `meta` properties would not properly show up in the Web UI
* Fixed a bug that would show the IBM footer in non-IBM environments.
* Fixed a bug where the time scrubber would display local time even when time preferences are set to UTC
* Fixed a bug where syntax highlighting in the search bar would not highlight correctly for certain queries
* Fixed a bug where logging in while trying to visit a URL would not redirect you to the correct URL after log in
* Fixed a bug where natural language time range search would not parse and search correctly for certain queries
* Fixed a bug where filter dropdown title disappears if there's not available filter options
* Updated in-app documentation to point to the correct Akamai URL configuration

## Enhancements
* Truncate long log level filters so long log levels don't disrupt the filter UI.




## LogDNA Agent v1.6.5

## Changed
Update internal logging [#164](https://github.com/logdna/logdna-agent/pull/164)

## Bugs
* Fix stringification issue on handling 207 [#152](https://github.com/logdna/logdna-agent/pull/152)
* Fix memory leak issue [#157](https://github.com/logdna/logdna-agent/pull/157)
* Make sure `process.getuid` doesn't get called on Windows [#188](https://github.com/logdna/logdna-agent/pull/188)

## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (now removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

