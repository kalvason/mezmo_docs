---
type: page
title: Mezmo Agent 3.5 (Beta)
listed: true
slug: mezmo-agent-3-5--beta-
description: 
index_title: Mezmo Agent 3.5 (Beta)
hidden: 
keywords: 
tags: 
---


## Mezmo Agent 3.5 Beta release notes

Mezmo is pleased to announce the Beta release of the Mezmo Agent version 3.5
Mezmo Agent runs on Kubernetes, Red Hat OpenShift, and now with this release, Linux (see our [Agent Support Matrix](https://docs.logdna.com/docs/logdna-agent-support-matrix)). To learn more about the Mezmo Agent version 3.5 Beta, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2/tree/3.5.0-beta.1).

New features and enhancements in the 3.5 Beta release:

- Configuration to omit sending metadata (ex. pod, namespace, container, etc.)
- Configuration to utilize leases on startup to stagger kube-api calls
- Fixed Kubernetes Enrichment panic when Kubernetes apiserver does something unexpected
- Rocksdb cache set to a 500KB