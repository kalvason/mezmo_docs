---
type: page
title: Mezmo Agent Support Matrix
listed: true
slug: mezmo-agent-support-matrix
description: Detailing our End of Life and End of Support Life support for the Mezmo Agent.
index_title: Mezmo Agent Support Matrix
hidden: 
keywords: 
tags: 
---




This article provides information about the supported platforms and operating systems (OS) for our [Mezmo Agents](/docs/introducing-the-agent), and the declared End of Life (EOL) and End of Support Life (EOSL) for each.

## How can I check what version of Mezmo Agent I am running?

For Agent v1 (Node Legacy Agent), the version is printed on agent startup. For Agent v2 (Rust Agent), the version is in the header of each log.

## What is End of Life (EOL)?

When a product reaches EOL, Mezmo will no longer be providing additional fixes or changes specific to that particular OS or platform version. Mezmo will continue to provide support when it comes to installing and using that particular piece of software.

## What is End of Support Life (EOSL)?

When a product reaches EOSL, Mezmo will no longer be providing any type of support for customers on that particular OS or platform version. Most likely the OS or platform version has been deprecated for some time and has also reached EOSL.

## Operating Systems Support Matrices

### Ubuntu




{% table %}
| Agent version | Ubuntu 16 | Ubuntu 18 | Ubuntu 20 | Ubuntu 20 | 
| ---- | ---- | ---- | ---- | ---- | 
| Rust Agent 3.3+\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nNode Agent 1.6.5+ | EOL: April 30, 2021\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: April 30, 2023 | EOL:  April 30, 2023\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: April 30, 2025 | TBA | 
{% /table %}

### Debian




{% table %}
| Agent version | Debian 8 | Debian 9 | Debian 10 | 
| ---- | ---- | ---- | ---- | 
| Rust Agent 3.3+\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nNode Agent 1.6.5+ | EOL: June 30, 2020\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: June 30, 2022 | EOL: January 31, 2022\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: TBA | TBA | 
{% /table %}

### CentOS




{% table %}
| Agent version | CentOS 7 | CentOS Linux 8 | CentOS Stream 8 | 
| ---- | ---- | ---- | ---- | 
| Rust Agent 3.3+\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nNode Agent 1.6.5+ | EOL: August 6, 2020\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: June 30, 2024 | EOL: December 31, 2021\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: June 31, 2022 | TBA | 
{% /table %}

### Red Hat Enterprise Linux (RHEL)




{% table %}
| Agent version | RHEL 7 | RHEL 8 | 
| ---- | ---- | ---- | 
| Rust Agent 3.3+\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nNode Agent 1.6.5+ | EOL: August 6, 2020\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: June 30, 2024 | TBA | 
{% /table %}

### Kubernetes




{% table %}
| Agent version | K8s v1.9 - 1.18 | K8s v1.19+ | K8s v1.17+ | 
| ---- | ---- | ---- | ---- | 
| Rust Agent 3.0+\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nNode Agent 1.6.5+ | EOL: November 1, 2021\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: April 1, 2022 | TBA | 
{% /table %}

### OpenShift




{% table %}
| Agent version | OpenShift 4.6 | OpenShift 4.7 | OpenShift 4.8 | 
| ---- | ---- | ---- | ---- | 
| Rust Agent 3.0+ | EOL: March 23, 2021\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: TBA | EOL: August 26, 2021\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: TBA | EOL: TBA\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nEOSL: TBA | 
{% /table %}

### AArch64/ARM64




{% table %}
| Agent version | 
| ---- | 
| Rust Agent 3.3+ | 
{% /table %}

Some additional notes:

- We deprecated support of sending logs via Websockets with versions starting from Agent v1.6. For prior versions of Agent the EOL for Websockets is November 1, 2020 and the EOSL for Websockets is April 1, 2021.
- All Agents older than Agent 1.6 are no longer supported and have reached EOSL





