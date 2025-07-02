---
type: page
title: Nov 4th, 2020 - LogDNA Web Version 4.13.1
listed: true
slug: nov-4th-2020-logdna-web-version-4131
description: 
index_title: Nov 4th, 2020 - LogDNA Web Version 4.13.1
hidden: 
keywords: 
tags: 
---




## Bugs
* Fixed a bug that would occasionally hide date markers in Timeline.
* Fixed a bug where the top of the log viewer would be cut off.
* Fixed a bug where "Jump to timeframe" example links would not work properly.
* Fixed space styling issues in the Usage Dashboard.



## LogDNA Terraform Provider v1.0.0

## Added
- Released our Terraform Provider in public beta. The Provider allows users to configure LogDNA Views and View-Specific Alerts via Terraform. Find the [documentation here](https://docs.logdna.com/docs/terraform-provider).


## LogDNA Agent v2.1.0 for Linux, Mac, and Windows

## Deprecated
* Deprecate WinEvent Logging support.
* Kubernetes support is completely moved to our [Rust-based Kubernetes agent](https://github.com/logdna/logdna-agent-v2). Kubernetes support is deprecated from our Linux, Mac and Windows agent.

## Changed
* Use `@logdna/logger-node` for logging.
* Use `systemd` service name as the app name for `journald` logs.
* Packages are built on Node v12.16.2 for all platforms except RedHat (due to CentOS 7 and RHEL 7 incompatibility).



## Changelog Categories
* Added (new features)
* Changed (changes in existing functionality)
* Removed (recently removed features)
* Deprecated (soon to be removed features)
* Fixed (bug fixes)
* Stability (vulnerabilities update)
* Enhancements (improved features)

