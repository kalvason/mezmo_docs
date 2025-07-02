---
type: page
title: LogDNA Agent for Kubernetes and OpenShift v3.1 (GA)
listed: true
slug: logdna-agent-for-kubernetes-and-openshift-v31-ga
description: 
index_title: LogDNA Agent for Kubernetes and OpenShift v3.1 (GA)
hidden: 
keywords: 
tags: 
---




## Release Notes



## May 10th, 2021


LogDNA is pleased to announce the GA (general availability) release of the LogDNA Agent for Kubernetes and OpenShift, version 3.1.

LogDNA Agent runs on Kubernetes (version 1.9 or later) or Red Hat OpenShift (version 4.5 or later). For more detailed information about the LogDNA Agent for Kubernetes and Openshift, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-agent-v2).

## New features and enhancements

-   The **lookback** functionality in the agent has been improved to provide the option of a "stateful", or persistent, collection of files that can be referenced whenever the agent is restarted, in order to return (or look back) to see any files that were ingested during the time that the agent was not running. This creates an optimal upgrade path for users. When upgrading from 3.0 to 3.1, the state file will be empty so the `lookback` setting will be used for existing files. After that (i.e. on process restart), the state file will be present and is used. For details, read our [documentation about configuring lookback](https://github.com/logdna/logdna-agent-v2/blob/3.1/docs/README.md#configuring-lookback).

-   Helm Charts are now available to deploy the LogDNA Agent in your Kubernetes cluster.
Helm is a package manager for Kubernetes, and you can use a Helm Chart, defined in a package containing a set of YAML files, as a single point of authority to provide repeatable build and deploy tasks to define, install, and upgrade Kubernetes resources. Refer to our [documentation about using Helm](https://github.com/logdna/logdna-agent-v2/blob/3.1/docs/HELM.md).


## Fixed Issues


-   We fixed an issue in which the agent panicked if it tried to open a file that does not exist (e.g. if it's created and destroyed before the `create` command is processed). \[LOG-8995\]



