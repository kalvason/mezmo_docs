---
type: page
title: LogDNA Agent for Kubernetes and OpenShift v3.2 (Beta)
listed: true
slug: logdna-agent-for-kubernetes-and-openshift-v32-beta
description: 
index_title: LogDNA Agent for Kubernetes and OpenShift v3.2 (Beta)
hidden: 
keywords: 
tags: 
---




## Release Notes


## May 27th, 2021


LogDNA is pleased to announce the Beta release of the LogDNA Agent for Kubernetes and OpenShift, version 3.2.

LogDNA Agent runs on Kubernetes (version 1.9 or later) or Red Hat OpenShift (version 4.5 or later). For more detailed information about the LogDNA Agent for Kubernetes and Openshift, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2).

## New features and enhancements


-   Using regex (regular expression) patterns, you can define rules to redact certain parts of log lines (such as sensitive PII data) before they leave the environment or premises. You can also use regex patterns to include _only_ specific lines, or exclude specific lines, and further control the log data that you want to send to LogDNA. For details, read our [documentation about using regex patterns](https://github.com/logdna/logdna-agent-v2/blob/3.2/docs/README.md#configuring-regex-for-redaction-and-exclusion-or-inclusion) and our library of common [regex patterns](https://github.com/logdna/logdna-agent-v2/blob/3.2/docs/REGEX.md).

## Fixed Issues


-   Kubernetes watch error: in previous versions, the agent repeatedly retried Kubernetes API watch errors until a successful response, causing unexpected resource usage when Kubernetes API was unavailable or unreachable. Now in Agent version 3.2, when Kubernetes API watch error is encountered, the agent will use an exponential backoff algorithm to decrease the rate of retries until a successful API response. \[LOG-8887\]

