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

Mezmo Kubernetes Enrichment centralizes Kubernetes events, resource metrics, and logs behind a single pane of glass to enable end-to-end visibility into your Kubernetes cluster. With Kubernetes Enrichment, you can troubleshoot deployment issues from within the Log Viewer, and view and set alerts for events like crashing pods or failing health checks in your production environments.

## Kubernetes Events

Knowing what is happening in your cluster alongside of your application log lines can be a valuable tool in debugging problems in your deployments.  With the Mezmo Agent, you can now do this.  

{% image url="https://uploads.developerhub.io/prod/2KW7/bjge4x9ig7imaygpjkrq6px4ezk6gx4m7oxuh0yd9w4j0dw444smb5xe1adynwq3.png" mode="full" height="365" width="821" %}
{% /image %}

To set this up in your cluster, head over to our [setup instructions on GitHub](https://github.com/logdna/logdna-agent-v2/blob/master/docs/KUBERNETES.md#enabling-k8-events).

## Kubernetes Metrics Reporter Enriched Lines

{% synced id="enteprisebanner" %}
{% /synced %}

{% callout type="warning" title="Upgrade to Mezmo Agent 3.7+" %}
The previous Mezmo Reporter that enabled metrics collection will soon be deprecated. We recommend all users to upgrade to the latest 3.7+ Mezmo Agent with built-in metrics support.
{% /callout %}

If you would like to see more detailed statistics about the pod your application is running on, edit your YAML config to enable metrics collection.  With this feature, you can correlate performance issues with log lines that may be causing those issues. Please note that non-enterprise customers will still incur the costs of storing metrics, but without the ability to see the metrics in Log Viewer.

After you enabling this feature, you can start viewing Kubernetes metrics in the Log Viewer. These metrics and metadata all show a point-in-time capture of the Kubernetes cluster state when that log line was sent, so even if an event happened a few days ago, the metrics will still reflect what was happening during that event.

1. In the Mezmo Web App, under **Views**, select a view that contains lines from your Kubernetes cluster.
2. Click the arrow next to a log line to open the information pane for that line.
3. Click the arrow next to **Kube Stats** to view metrics including CPU usage and memory for the pod and node associated with the log entry. All metrics have the same retention as your log retention, and metrics are collected every 30 seconds.

{% image url="https://uploads.developerhub.io/prod/2KW7/x5m81etb84rvddog2a0rvecoypvt4vllg28ibredgt16ej4e6cgfdy53lzqrp8e9.png" caption="Collapsed view of Kube Stats" mode="full" height="205" width="1051" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/2KW7/2b3j4q9k4c1j0nqm83zbma70r71gi5ae86blszc3lcud6ts1frydbyxj4fplgmts.png" caption="Expanded view of Kube Stats" mode="full" height="584" width="1176" %}
{% /image %}

Other information you can view includes:

- Events associated with the log line
- Line identifiers
- Labels
- Diagnostics