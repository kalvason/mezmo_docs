---
type: page
title: View Kubernetes Events and Metrics
listed: true
slug: kubernetes-enrichment
description: 
index_title: View Kubernetes Events and Metrics
hidden: 
keywords: 
tags: 
---

{% synced id="enteprisebanner" %}
{% /synced %}

Mezmo Kubernetes Enrichment centralizes Kubernetes events, resource metrics, and logs behind a single pane of glass to enable end-to-end visibility into your Kubernetes cluster. With Kubernetes Enrichment, you can troubleshoot deployment issues from within the Log Viewer, and view and set alerts for events like crashing pods or failing health checks in your production environments.  

## Pre-Requisites

- Kubernetes version 1.9+
- Mezmo Agent for Kubernetes installed and running in your cluster
- [Kubernetes Metrics Server](#verifying-installation-of-the-kubernetes-metrics-server) installed on your Kubernetes cluster
- Mezmo Reporter (contact your Customer Success Manager for installation instructions)

## Verify Installation of the Kubernetes Metrics Server

The Kubernetes Metrics Server is installed by default if you’re using Google Kubernetes Engine (GKE), IBM Cloud Kubernetes Service, or Azure Kubernetes Service (AKS) of at least version 1.10.

For other providers you can find instructions on how to install `metrics-server` here:

- [AWS Elastic Kubernetes Service](https://docs.aws.amazon.com/eks/latest/userguide/metrics-server.html)
- [IBM Kubernetes Service](https://cloud.ibm.com/catalog/content/metrics-server)
- [Kubernetes Installation Manifest](https://github.com/kubernetes-sigs/metrics-server#deployment)

To verify if you have `metrics-server` installed, run this command:

{% code %}
{% tab language="none" %}
kubectl get deployment metrics-server -n kube-system
{% /tab %}
{% /code %}

If `metrics-server`is installed, you will see this output:

{% code %}
{% tab language="none" %}
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
metrics-server   1/1     1            1           9s
{% /tab %}
{% /code %}

## View Kubernetes Events and Metrics

After you deploy the Mezmo Reporter, you can start viewing Kubernetes events and metrics in the Log Viewer. These metrics and metadata all show a point-in-time capture of the Kubernetes cluster state when that log line was sent, so even if an event happened a few days ago, the metrics will still reflect what was happening during that event.

1. In the Mezmo Web App, under **Views**, select an event type from the **Kube Events** views. 
2. Click the arrow next to a log line to open the information pane for that line. 
3. Click the arrow next to **Kube Stats** to view metrics including CPU usage and memory for the pod and node associated with the log entry. All metrics have the same retention as your log retention, and metrics are collected every 30 seconds.

{% image url="https://uploads.developerhub.io/prod/2KW7/538o8ki385v6z2j3dldr1x9ict3kzvxl9ny8ilzx0fkvo9b1ddvvip9qe2vdvuyn.png" caption="Pod Metrics for a Kubernetes event" mode="full" height="704" width="1996" %}
{% /image %}

Other information you can view includes:

- Events associated with the log line
- Line identifiers
- Labels
- Diagnostics

{% callout type="info" title="View Events in Context" %}
Use the **View In Context** option to see the log lines preceding a specific event, for example what an application was logging before it was killed.
{% /callout %}

## Kube Events Views

The events you can view through **Kube Events** include:

- Jobs Lifecycle
- Kube System
- Nodes NotReady

- Pods Crashing
- Pods Lifecycle

- Probes Failing
- Runtime Errors

- Scaling Events
- Scheduling Errors

- Warnings
- Warnings (&gt;x100)

- Warnings (&gt;x1000)