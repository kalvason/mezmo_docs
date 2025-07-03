---
type: page
title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (v2.2.2, 3.0.2 )
listed: true
slug: agent-hot-fix-bulletin-2-2-2-and-3-0-2
description: 
index_title: Hot Fix Bulletin, LogDNA Agent for Kubernetes and OpenShift (v2.2.2, 3.0.2 )
hidden: 
keywords: 
tags: 
---


## Summary

This hotfix (patch release versions 2.2.2 and 3.0.2) includes code to resolve known issues with the LogDNA Agent for Kubernetes and OpenShift.

## Filesystem Storage Issue

- ## How was the issue manifested?

After a log file was deleted, the agent held a descriptor to the file preventing the storage on the filesystem to be freed.

- ## What was the resolution?

We added additional handling to make sure internal references to the file descriptor are dropped.

## Spurious errors from the Kubernetes API

- ## How was the issue manifested?

Previously when the Kubernetes event endpoint returned a "too old resource version” error the agent would panic and restart in order to ensure its internal state was valid.

- ## What was the resolution?

The agent will now automatically repopulate its state when it encounters this error.

#How do I apply the patch?
The patch is available in our GitHub repository. Refer to the &lt;a href="[https://github.com/logdna/logdna-agent-v2#installing"](https://github.com/logdna/logdna-agent-v2#installing&quot;) target="_blank"&gt;installation instructions&lt;/a&gt; in the Readme.md file.


{% callout type="info" title="Info" %}
[Version 2.2.2 https://github.com/logdna/logdna-agent-v2/releases/tag/2.2.2](https://github.com/logdna/logdna-agent-v2/releases/tag/2.2.2) [Version 3.0.2: https://github.com/logdna/logdna-agent-v2/releases/tag/3.0.2](https://github.com/logdna/logdna-agent-v2/releases/tag/3.0.2)
{% /callout %}


NOTE: To update your existing deployments, edit the container image in the LogDNA daemonset manifest to point to 2.2.2 or 3.0.2 depending on your current version.

## Support

Please reach out to the LogDNA Support team if you have further questions. You can use the Contact Support option in the LogDNA application (Settings -&gt; Contact Support) or open a ticket for your account.

