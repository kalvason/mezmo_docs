---
type: page
title: July 22nd, 2020 - LogDNA Web Version 2.26.0
listed: true
slug: july-22nd-2020-logdna-web-version-2261
description: 
index_title: July 22nd, 2020 - LogDNA Web Version 2.26.0
hidden: 
keywords: 
tags: 
---



## Bugs
- Fixed a bug that prevented meta values passed as string from being ingested properly
- Fixed a bug where having multiple JSON objects passed in a log line would fail to parse properly.
- Fixed a bug where searching by time would have the log viewer jump to the incorrect log line.
- Fixed a bug where if the parser fails to parse a line, a particular edge case would prevent the parser error from being surfaced.

## Enhancements
- Improved error handling when histogram fails to load.
- Improved when an timeout happens during a search, existing search results will still show in the log viewer.


## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (now removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

