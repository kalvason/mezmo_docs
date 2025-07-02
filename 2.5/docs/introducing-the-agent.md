---
type: page
title: Mezmo Logging Agent
listed: true
slug: introducing-the-agent
description: You can install the Mezmo Logging Agent on a host and it will automatically send log data to Mezmo
index_title: Mezmo Logging Agent
hidden: 
keywords: 
tags: 
---

The Mezmo Agent reads log files from the host where it is installed, and uploads the log data to Mezmo via a secure HTTPS connection, where it is parsed and processed according to the parameters you have set in the Mezmo Agent configuration file. The Mezmo Agent runs on Kubernetes, Openshift, Linux, Windows, and MaxOS. This topic describes the two versions of the Mezmo Agent, and includes links to the GitHub repositories and release versions for both versions.

## Version 1

Version 1 of the Mezmo Logging Agent is developed for use on **Linux**, **Windows**, and **macOS**. If you want to send log data from a Windows host, we recommend that you use this version of the Mezmo Logging Agent.

### GitHub Repository

For complete information about installing and configuring the Mezmo Agent v1, check out the source code and documentation in our GitHub repository.
[https://github.com/logdna/logdna-agent](https://github.com/logdna/logdna-agent)

Starting from Agent v1 3.6 GA, we recommend upgrading to Version 2, which is a more performant Agent that can handle all the types of logs supported by Version 1.

## Version 2

The Mezmo Agent v2 is written in Rust, and uses the Linux kernel to monitor the log files and directories for changes, rather than having to poll these files constantly. This implementation frees up CPU utilization and improves stability. It is developed for use on **Linux**, **Kubernetes**, and **Red Hat**. Mezmo plans to migrate to Agent v2 completely, including for Windows installations.

### GitHub Repository

For complete information about installing and configuring the Mezmo Agent V2, check out the source code and documentation in our GitHub repository.
[https://github.com/logdna/logdna-agent-v2](https://github.com/logdna/logdna-agent-v2)

### Release Notes

- [Mezmo Agent v3.5 (GA)](https://docs.mezmo.com/changelog/logdna-agent-35-ga)
- [Mezmo Agent v3.5 (Beta)](https://docs.mezmo.com/changelog/logdna-agent-35-beta)
- [Mezmo Agent v3.4 (GA)](https://docs.mezmo.com/changelog/logdna-agent-34-ga)
- [Mezmo Agent v3.3 (GA)](https://docs.mezmo.com/changelog/logdna-agent-33-ga)
- [Mezmo Agent v3.3 (Beta)](https://docs.mezmo.com/changelog/logdna-agent-33-beta)
- [Mezmo Agent v3.2 (GA)](https://docs.mezmo.com/changelog/logdna-agent-for-kubernetes-and-openshift-v32-ga)
- [Mezmo Agent v3.2 (Beta)](https://docs.mezmo.com/changelog/logdna-agent-for-kubernetes-and-openshift-v32-beta)
- [Mezmo Agent v3.1 (GA)](https://docs.mezmo.com/changelog/logdna-agent-for-kubernetes-and-openshift-v31-ga))
- [Mezmo Agent v3.1 (Beta](https://docs.mezmo.com/changelog/logdna-agent-for-kubernetes-and-openshift-v31-beta)
- [Mezmo Agent v3.0 (GA)](https://docs.mezmo.com/changelog/logdna-agent-for-kubernetes-and-openshift-v3-0)

## Mezmo Agent FAQS

### How do I tell the Mezmo Agent what to log?

By default, the Mezmo Agent automatically logs all .log and extensionless files located under /var/log/, but if you want to log other directories or files, you can use these commands in a host terminal to specify additional directories or files:

For directories:

{% code %}
{% tab language="bash" %}
sudo LogDNA-agent -d "/path/to/my/logs"
{% /tab %}
{% /code %}

For files:

{% code %}
{% tab language="bash" %}
sudo LogDNA-agent -f "/path/to/my/logfile"
{% /tab %}
{% /code %}

If you need more complex logic, you can also view and set specific logging paths, as well as use glob patterns by editing `/etc/LogDNA.conf` or /etc/LogDNA.env`, depending on the agent version.

### Is the Mezmo Agent open source?

Yes! You can view, and contribute to, the source code on GitHub for both Agentv1 and Agent v2, and even build the agent yourself.

We also love the open source community, so please feel welcome to submit PRs or report any issues you find. Check out our contributing guide for more info.

### How do I use host tags?

Host tags let you automatically group hosts into dynamic host groups without having to explicitly assign a host to a group within the Mezmo web app. To use tags, make sure the agent is installed on your host, and use this command to add a tag or tags:

{% code %}
{% tab language="bash" %}
sudo LogDNA-agent -t mytag,myothertag,anothertag
{% /tab %}
{% /code %}

You can also edit the LogDNA configuration file, `etc/LogDNA.conf` or /etc/LogDNA.env, depending on the agent version, and specify the tags there.

Even if your hostname or host machine changes, as long as the agent is running with the same tags configured, that host will automatically be added to the dynamic group located under the **Hosts** filter.

### How do I override the default hostname?

The Mezmo agent automatically uses the machine's default OS hostname. If you wish to use a different hostname, you can edit the LogDNA configuration file, `/etc/LogDNA.conf` or /etc/LogDNA.env`, depending on the agent version,  and specify the hostname there.

### Why Does the Mezmo Agent v1 need root access?

The Mezmo Agent v1 works by monitoring changes in local log files (read only access) and sending new lines to the designated ingestion endpoint.

These are the primary reasons why Mezmo's agent requires root access:

1. The agent listens to kernel-level file events to detect new lines in log files.
2. The agent monitors default log file paths, such as `/var/log` or `/var/data`.
3. Container-based frameworks such as Kubernetes also use these file paths.

Kubernetes centralized logging, which writes all container logs to `/var/log`, recommends using a DaemonSet and node-level logging, which is how we implemented the Mezmo agent.