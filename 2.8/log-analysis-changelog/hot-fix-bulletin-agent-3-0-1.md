---
type: page
title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (2.2.1 and 3.0.1)
listed: true
slug: hot-fix-bulletin-agent-3-0-1
description: 
index_title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (2.2.1 and 3.0.1)
hidden: 
keywords: 
tags: 
---





## Summary
This hot fix (patch release versions 2.2.1 and 3.0.1) includes code to resolve a known issue with the LogDNA Agent for Kubernetes and OpenShift. The fix has been applied to all of our our self-serve and SaaS environments.


## How was the issue manifested?
Dangling symlinks were causing the Agent to crash, specifically in versions 2.2 and 3.0 of the Agent.


## What was the resolution?
The crash was caused by invalid state in the agent's filesystem cache, triggered by the existence of dangling symlinks on the filesystem. The fs cache has been updated to handle this case and to fail more gracefully in general.

#How do I apply the patch?
The patch is available in our GitHub repository. Refer to the &lt;a href="https://github.com/logdna/logdna-agent-v2#installing" target="_blank"&gt;installation instructions&lt;/a&gt; in the Readme.md file.


{% callout type="info" title="Info" %}
Version 2.2.1: https://github.com/logdna/logdna-agent-v2/releases/tag/2.2.1
Version 3.0.1: https://github.com/logdna/logdna-agent-v2/releases/tag/3.0.1
{% /callout %}




## Support
Please reach out to the LogDNA Support team if you have further questions. You can use the Contact Support option in the LogDNA application (Settings -&gt; Contact Support) or open a ticket for your account.

