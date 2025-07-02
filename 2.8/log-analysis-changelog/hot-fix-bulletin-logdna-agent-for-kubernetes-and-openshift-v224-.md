---
type: page
title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (v2.2.4, 3.0.4)
listed: true
slug: hot-fix-bulletin-logdna-agent-for-kubernetes-and-openshift-v224-
description: 
index_title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (v2.2.4, 3.0.4)
hidden: 
keywords: 
tags: 
---





## Summary
This hotfix (patch release versions 2.2.4 and 3.0.4) resolves a known issue with the LogDNA Agent for Kubernetes and OpenShift.


## Logs being dropped slowly over time

## What was the issue?
The LogDNA Agent eventually stopped gathering and sending logs to LogDNA.

## What was the resolution?

We fixed an incorrect loop termination condition and a potential race condition that prevented the LogDNA Agent from processing log files that were added after initialization.

#How do I apply the patch?
The patch is available in our GitHub repository. Refer to the &lt;a href="https://github.com/logdna/logdna-agent-v2#installing" target="_blank"&gt;installation instructions&lt;/a&gt; in the Readme.md file.


{% callout type="info" title="Info" %}
Version 2.2.4: https://github.com/logdna/logdna-agent-v2/releases/tag/2.2.4
Version 3.0.4: https://github.com/logdna/logdna-agent-v2/releases/tag/3.0.4
{% /callout %}




## Support
If you have support-related questions about any of the above features or fixes, please reach out to us at [support@logdna.com](mailto:support@logdna.com).

