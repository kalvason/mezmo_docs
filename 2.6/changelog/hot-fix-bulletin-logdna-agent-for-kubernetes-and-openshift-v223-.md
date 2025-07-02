---
type: page
title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (v2.2.3, 3.0.3)
listed: true
slug: hot-fix-bulletin-logdna-agent-for-kubernetes-and-openshift-v223-
description: 
index_title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (v2.2.3, 3.0.3)
hidden: 
keywords: 
tags: 
---




## Summary
This hot fix (patch release versions 2.2.3 and 3.0.3) includes code to resolve a known issue with the LogDNA Agent for Kubernetes and OpenShift.


## Gradual log loss in Agent as log files were rotated

## How was the issue manifested?
Depending on the timing of **inotify** events during log rotation, the agent did not pick up the rotated files due to events being processed in the wrong order.

## What was the resolution?

The **inotify** events are now buffered across **inotify** calls to ensure that filesystem events are processed in the correct order, and to ensure that log files are picked up after being rotated.

#How do I apply the patch?
The patch is available in our GitHub repository. Refer to the &lt;a href="https://github.com/logdna/logdna-agent-v2#installing" target="_blank"&gt;installation instructions&lt;/a&gt; in the Readme.md file.


{% callout type="info" title="Info" %}
Version 2.2.3: https://github.com/logdna/logdna-agent-v2/releases/tag/2.2.3
Version 3.0.3: https://github.com/logdna/logdna-agent-v2/releases/tag/3.0.3
{% /callout %}




## Support
Please reach out to the LogDNA Support team if you have further questions. You can use the Contact Support option in the LogDNA application (Settings -&gt; Contact Support), open a ticket for your account, or email us at [support@logdna.com](mailto:support@logdna.com).

