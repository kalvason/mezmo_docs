---
type: page
title: Mezmo Agent 3.3 (GA)
listed: true
slug: mezmo-agent-33-ga
description: 
index_title: Mezmo Agent 3.3 (GA)
hidden: 
keywords: 
tags: 
---

## Release Notes

[https://docs.mezmo.com/changelog/logdna-agent-33-ga#release-notes](https://docs.mezmo.com/changelog/logdna-agent-33-ga#release-notes)

## October 15th, 2021

[https://docs.mezmo.com/changelog/logdna-agent-33-ga#october-15th-2021](https://docs.mezmo.com/changelog/logdna-agent-33-ga#october-15th-2021)

Mezmo is pleased to announce the GA release of the Mezmo Agent version 3.3.

Mezmo Agent runs on Kubernetes, Red Hat OpenShift, and now with this release, Linux (see our [Agent Support Matrix](https://docs.logdna.com/docs/logdna-agent-support-matrix?__hstc=220250695.ba31ea1a08c89e25ee6fbaf2f53b3930.1655751609988.1657736784060.1657742944328.5&amp;__hssc=220250695.1.1657742944328&amp;__hsfp=501963141)). To learn more about the Mezmo Agent version 3.3 GA, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2/tree/3.3.0).

## New features and enhancements in the 3.3 GA release

[https://docs.mezmo.com/changelog/logdna-agent-33-ga#new-features-and-enhancements-in-the-33-ga-release](https://docs.mezmo.com/changelog/logdna-agent-33-ga#new-features-and-enhancements-in-the-33-ga-release)

- **Linux support**: This release provides support for Linux, and is intended to eventually supplant the earlier, legacy, Node.js agent for Linux. For instructions for migrating from the legacy Linux agent, refer to the [documentation](https://github.com/logdna/logdna-agent-v2/blob/3.3/docs/LINUX.md).
- **Metrics**: The Mezmo agent records metrics that are relevant for monitoring and alerting, such as number log files currently tracked or number of bytes parsed, along with process status information. To access these metrics, enable the agent's Prometheus endpoint to expose the internal metrics to a Prometheus server. Read more about accessing these metrics in our [documentation](https://github.com/logdna/logdna-agent-v2/blob/3.3/docs/INTERNAL_METRICS.md).
- **AArch64/ARM64 support**: LogDNA Agent 3.3 GA runs on AArch64/ARM64 systems.