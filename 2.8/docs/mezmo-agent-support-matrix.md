---
type: page
title: Mezmo Agent Supported Platforms
listed: true
slug: mezmo-agent-support-matrix
description: Detailing our End of Life and End of Support Life support for the Mezmo Agent.
index_title: Mezmo Agent Supported Platforms
hidden: 
keywords: 
tags: 
---

This article provides information aboutthe supported platforms for our [Mezmo Agents](/docs/introducing-the-agent).

## What is End of Life (EOL)?

When a platform reaches its End of Life (EOL), Mezmo will no longer be providing additional fixes or changes specific to that particular OS or platform version. Mezmo adheres to the EOL dates established by the OS/platform maintainers.

## Supported Platforms

- Ubuntu ([Ubuntu EOL Lifecycle](https://ubuntu.com/about/release-cycle))
- Debian ([Debian EOL Lifecycle](https://endoflife.software/operating-systems/linux/debian))
- CentOS ([CentOS EOL Lifecycle](https://endoflife.date/centos))
- Red Hat Enterprise Linux/RHEL ([RHEL EOL Lifecycle](https://access.redhat.com/support/policy/updates/errata))
- Kubernetes ([Kubernetes EOL Lifecycle](https://endoflife.date/kubernetes))
- Windows ([Windows EOL Lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/windows-10-enterprise-and-education))
- OpenShift ([OpenShift EOL Lifecycle](https://access.redhat.com/support/policy/updates/openshift))
- Linux architectures available: AMD64 and ARM64 

Installation instructions for the specified platform/OS are available on our [Github](https://github.com/logdna/logdna-agent-v2/tree/master?tab=readme-ov-file#managing-deployments).

## Additional Notes

- Sending logs via Websockets is no longer supported (EOL November 1, 2020).
- ppc64 architecture is not supported.