---
type: page
title: Mezmo Edge Pipelines for Local Data
listed: true
slug: mezmo-edge-pipelines-for-local-data
description: 
index_title: Mezmo Edge Pipelines for Local Data
hidden: 
keywords: 
tags: 
---

Mezmo Edge lets you run a telemetry data pipeline within your environment that has the same functionality available within your Mezmo Telemetry Pipeline cloud environment, but adds its own capabilities for processing your data locally. You can run any Pipeline as a satellite node within an Edge instance. All of the metrics and management of the Pipeline are still handled by the SaaS infrastructure, making it easy to build, test, and deploy without requiring any additional coding or configuration management.

Mezmo Edge can be deployed to any Kubernetes cluster using [a Helm chart](https://helm.sh/docs/intro/quickstart/), as explained in the topic [auto$](/mezmo-edge/set-up-mezmo-edge-in-kubernetes). Mezmo Edge uses **Horizontal Pod Autoscaling (HPA)** to scale to your workloads, which means you can take advantage of the scalability Kubernetes offers without having to invest substantial time and effort to manage the scaling.

## What's New in Mezmo Edge

Because Mezmo Edge is entirely contained and running within your infrastructure, if offers several capabilities for managing and processing your data. These include:

- Accessing local data sources without any changes to your networking, such as punching holes in firewalls
- Processing and sending data entirely within your local network
- Sending raw syslog directly to your pipelines without needing any additional security plugins
- Leveraging the full power of regular expressions (regex) within your pipeline

{% callout type="success" title="RegEx Syntax Based on Rust" %}
The regex syntax for Mezmo Edge is based on the Rust implementation of RegEx. This regex syntax  is similar to other regex engines, but it lacks several features that cannot be efficiently implemented. This includes look-around and back references. However, all Rust regex searches have worst case `O(m * n)` time complexity, where `m` is proportional to the size of the regex and `n` is proportional to the size of the string being searched. You can find more information [in the Rust documentation](https://docs.rs/regex/latest/regex/).
{% /callout %}