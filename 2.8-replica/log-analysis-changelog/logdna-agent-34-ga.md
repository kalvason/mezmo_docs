---
type: page
title: LogDNA Agent 3.4 (GA)
listed: true
slug: logdna-agent-34-ga
description: 
index_title: LogDNA Agent 3.4 (GA)
hidden: 
keywords: 
tags: 
---





## Release Notes

## March 22nd, 2022

LogDNA is pleased to announce the GA release of the LogDNA Agent version 3.4.

LogDNA Agent runs on Kubernetes, Red Hat OpenShift, and now with this release, Linux (see our &lt;a href="https://docs.logdna.com/docs/logdna-agent-support-matrix" target="_blank"&gt;Agent Support Matrix&lt;/a&gt;). To learn more about the LogDNA Agent version 3.4 GA, refer to the documentation in our public &lt;a href="https://github.com/logdna/logdna-agent-v2/tree/3.4.0" target="_blank"&gt;GitHub repository&lt;/a&gt;.

## New features and enhancements in the 3.4 GA release

* Longer backoff for HTTP 5XX errors
* Immediate exiting on HTTP 4XX errors
* Recovery on inotify errors
* Configurable retry file locations
* Maximum retry file sizes
* Additional retry metrics
* Compressed retry files
* HTTP 2.0 support
* Concurrent uploads providing higher throughput and lower latency guarantees, especially for systems which experience high ingest latency



