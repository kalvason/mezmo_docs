---
type: page
title: Mezmo Agent 3.7 (GA)
listed: true
slug: mezmo-agent-3-7-ga
description: 
index_title: Mezmo Agent 3.7 (GA)
hidden: 
keywords: 
tags: 
---

## Mezmo 3.7 GA Notes

**Mezmo is pleased to announce the GA release of the Mezmo Agent version 3.7.** Mezmo Agent runs on Kubernetes, Red Hat OpenShift, Linux and Windows (see our [Agent Support Matrix](https://docs.mezmo.com/docs/mezmo-agent-support-matrix)). To learn more about the Mezmo Agent version 3.7 GA, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2/tree/3.7).

New features and enhancements in the 3.7 GA release:

- Inclusion of Kubernetes metrics enrichment. There is no longer a need to install the separate Mezmo reporter service. This Kubernetes enrichment capability is available only with Enterprise plan. For more information check out the [Kubernetes Enrichment](https://docs.mezmo.com/docs/kubernetes-enrichment) topic. If you are currently on an Enterprise plan and would like access to this feature, please contact your Customer Success Manager.
- Better resilience when the agent encounters file permission errors on first read attempt.