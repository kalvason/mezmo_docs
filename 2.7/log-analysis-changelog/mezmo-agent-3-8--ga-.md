---
type: page
title: Mezmo Agent 3.8 (GA)
listed: true
slug: mezmo-agent-3-8--ga-
description: 
index_title: Mezmo Agent 3.8 (GA)
hidden: 
keywords: 
tags: 
---

## Mezmo 3.8 GA Notes

**Mezmo is pleased to announce the GA release of the Mezmo Agent version 3.8.** Mezmo Agent runs on Kubernetes, Red Hat OpenShift, Linux and Windows (see our [Agent Support Matrix](https://docs.mezmo.com/docs/mezmo-agent-support-matrix)). To learn more about the Mezmo Agent version 3.8 GA, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2/tree/3.8.0).

New features and enhancements in the 3.8 GA release:

- Exclude/include logs from pods based on annotations and labels
- Collect image name and tag for containers as metadata for each log line
- FIX: Very frequent DNS requests made when requests to DNS service are rejected
- FIX: Advanced Glob and Regex patterns not recognized and causing files to be ignored