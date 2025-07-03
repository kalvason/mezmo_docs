---
type: page
title: LogDNA Agent for Kubernetes and OpenShift, version 3.0
listed: true
slug: logdna-agent-for-kubernetes-and-openshift-v3-0
description: 
index_title: LogDNA Agent for Kubernetes and OpenShift, version 3.0
hidden: 
keywords: 
tags: 
---





## Release Notes


## December 15th, 2020

LogDNA is pleased to announce the general availability release of the LogDNA Agent for Kubernetes and OpenShift, version 3.0.

LogDNA Agent runs on Kubernetes (version 1.9 or later) or Red Hat OpenShift (version 4.5 or later). For more detailed information about the LogDNA Agent for Kubernetes  and Openshift, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2).

## New features and enhancements
Note: These Release Notes reflect the same content as the v2.2 Beta release, as no user-facing changes were made.
* LogDNA Agent for Kubernetes and Openshift is now configurable to run as a non-root user. For details refer to our documentation on [Running as non-root](https://github.com/logdna/logdna-agent-v2/tree/3.0/docs/README.md#running-as-non-root).
*  Configuration for [Lookback](https://github.com/logdna/logdna-agent-v2/tree/3.0/docs/README.md#configuring-lookback) options for how the Agent handles files upon starting.
*  Enabling journald monitoring for [Kubernetes](KUBERNETES.md#collecting-node-journald-logs) or [OpenShift](OPENSHIFT.md#collecting-node-journald-logs).
* Logging Kubernetes events. See [Configuring Kubernetes Events](https://github.com/logdna/logdna-agent-v2/tree/3.0/docs/README.md#configuring-events)
* Base image of the Agent hosted on DockerHub is updated to UBI 8
* Kubernetes Labels support; log file's metadata is now enriched with Kubernetes labels.

## Changes
* Updated tagging scheme for the Agent image that is available on [DockerHub](https://hub.docker.com/r/logdna/logdna-agent).

## Known limitations
* With `lookback=start` the Agent will temporarily fully buffer files in memory before uploading; this may cause issues with log files that are larger than available memory.
*  When lookback is enabled pre-existing lines will be updated only after a change is detected in the file. If a file is completely static the lines will not be uploaded.
* Agent lookback does not track which lines have been uploaded, therefore log duplication may result if the agent is restarted with lookback enabled.
* The agent may generate many log entries when a file matching an ignore pattern is recreated or updated frequently. A workaround would be to configure the RUST_LOG environment variable to raise the log level to `warn, error` threshold.

