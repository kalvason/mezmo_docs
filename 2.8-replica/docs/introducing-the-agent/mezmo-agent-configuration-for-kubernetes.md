---
type: page
title: Mezmo Agent Configuration for Kubernetes
listed: true
slug: mezmo-agent-configuration-for-kubernetes
description: 
index_title: Mezmo Agent Configuration for Kubernetes
hidden: 
keywords: 
tags: 
---


When using the Mezmo Logging Agent within a Kubernetes cluster, the configuration is a bit different than the standard v2 agent configuration.

The only editable file is the `environmental variables `section of the `daemonset` configurations.

## To configure the agent

Find the effective config at beginning of agent pod log. It should look like this:

{% code %}
{% tab language="json" %}
http:
host: logs.logdna.com
endpoint: /logs/agent
use_ssl: true
timeout: 10000
use_compression: true
gzip_level: 2
params:
hostname: main-mac-ubuntu
mac: ~
ip: ~
tags: ~
body_size: 2097152
log:
dirs:
    - /home/dmitri/SOURCE/TMP/root/subdir_missing
include:
glob:
- "*.log"
regex: []
exclude:
glob: []
regex: []
lookback: start
log_metric_server_stats: ~
journald:
systemd_journal_tailer: ~
startup: {}
{% /tab %}
{% /code %}

Copy this config file and put it in a new text file, use vim `<name of file>` for example (depending on what text editor you use) Then to this file, you'll add the below params.

{% code %}
{% tab language="json" %}
http:
params:
retrybase delay_ms: 100000
retry_step_delay_ms: 10000
{% /tab %}
{% /code %}

Apply this config file to your Kubernetes cluster.

Then m[odify the envs section of the DaemonSet](https://github.com/logdna/logdna-agent-v2#configuring-the-environment)  you deployed with the env. variable `LOGDNA`_`CONFIG`_`FILE = <full_path_to_config_yaml>`