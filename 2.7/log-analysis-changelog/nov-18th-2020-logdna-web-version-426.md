---
type: page
title: Nov 18th, 2020 - LogDNA Web Version 4.26.8
listed: true
slug: nov-18th-2020-logdna-web-version-426
description: 
index_title: Nov 18th, 2020 - LogDNA Web Version 4.26.8
hidden: 
keywords: 
tags: 
---



## Bugs:
- Updated `syslog-ng` to have the correct logging directive in in-app docs
- Fixed a bug where muting an alert on a cloned alert would mute both the cloned and original alert.
- Fixed a bug where the view link for a muted alert in the alert settings page would link to an invalid URL.
- Fixed a bug where certain alerts would not be muteable.

## Changed:
- Allow member role users to add new Slack channels to the account.

## Added:
- Added alert threshold graph to visualize historical log volume trends versus alert threshold when creating or editing an alert.

## Enhancements:
- Improved CloudTrail app name parsing.
- Added "Only" filter functionality to Tags and Level filters.



## Agent v2.2 Public Beta

## Added:
- Kubernetes event support
- OpenShift support
- Journald support
- Running as non-root configuration
- Agent lookback configuration
- Base Image updated to UBI 8
- Kubernetes Labels support

## Bugs:
- Fixed instrumentation issue where `user-agent` was set to `agent`
For full specs, checkout our documentation: https://docs.logdna.com/docs/logdna-agent-v2-for-kubernetes


## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (recently removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

