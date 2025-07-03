---
type: page
title: LogDNA Agent 3.3 (Beta)
listed: true
slug: logdna-agent-33-beta
description: 
index_title: LogDNA Agent 3.3 (Beta)
hidden: 
keywords: 
tags: 
---



## Release Notes

[https://docs.mezmo.com/changelog/logdna-agent-33-ga#release-notes](https://docs.mezmo.com/changelog/logdna-agent-33-ga#release-notes)

## August 19, 2021

[https://docs.mezmo.com/changelog/logdna-agent-33-ga#august-19-2021](https://docs.mezmo.com/changelog/logdna-agent-33-ga#august-19-2021)

LogDNA is pleased to announce the Beta release of the LogDNA Agent version 3.3.

LogDNA Agent runs on Kubernetes, Red Hat OpenShift, and now with this release, Linux (see our [Agent Support Matrix](https://docs.logdna.com/docs/logdna-agent-support-matrix)). To learn more about the LogDNA Agent version 3.3 Beta, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2/tree/3.3.0-beta.1).

## New features and enhancements in the 3.3 Beta release

[https://docs.mezmo.com/changelog/logdna-agent-33-ga#new-features-and-enhancements-in-the-33-beta-release](https://docs.mezmo.com/changelog/logdna-agent-33-ga#new-features-and-enhancements-in-the-33-beta-release)

- **Linux support**: This release provides support for Linux, and is intended to eventually supplant the earlier, legacy, Node.js agent for Linux. For instructions for migrating from the legacy Linux agent, refer to the [documentation](https://github.com/logdna/logdna-agent-v2/blob/3.3/docs/LINUX.md).
- **Metrics**: The LogDNA agent records metrics that are relevant for monitoring and alerting, such as number log files currently tracked or number of bytes parsed, along with process status information. To access these metrics, enable the agent's Prometheus endpoint to expose the internal metrics to a Prometheus server. Read more about accessing these metrics in our [documentation](https://github.com/logdna/logdna-agent-v2/blob/3.3/docs/INTERNAL_METRICS.md).
- **AArch64/ARM64 support**: LogDNA Agent 3.3 Beta runs on AArch64/ARM64 systems.

