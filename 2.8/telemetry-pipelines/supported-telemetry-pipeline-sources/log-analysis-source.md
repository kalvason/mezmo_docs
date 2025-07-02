---
type: page
title: Mezmo Log Analysis
listed: true
slug: log-analysis-source
description: 
index_title: Mezmo Log Analysis
hidden: 
keywords: 
tags: 
---

{% callout type="error" title="Deprecated (Jan 30, 2025)" %}
This source is deprecated and will be removed in a future release (TBD). You can use the [auto$](/telemetry-pipelines/log-analysis-ingestion-source)  source as an alternative long-term supported source.

**NOTE:** as of Jan 30, 2025, this source is only available to customer organizations that had previously utilized it on a pipeline.
{% /callout %}

## Description

This source will allow your Log Analysis account to automatically forward received logs to this Pipeline.

There is no configuration for this source, it will simply send a copy of your log lines from your log analysis account to this pipeline without further configuration.

{% callout type="info" title="Single Source to Single Pipeline" %}
Your Log Analysis account can only be used as a single source to a single Pipeline within your account.
{% /callout %}

{% callout type="warning" title="Fully Excluded Lines Not Included" %}
Log lines that are preserved for Live Tail and Alerting will be included, but fully excluded lines aren't.
{% /callout %}

### Included metadata

By default, the Mezmo Log Analysis Source sends these fields in the metadata query object (e.g. `metadata.query.account` ):

{% table widths="273,0" %}
| Field | Type | Description | 
| ---- | ---- | ---- | 
| `account` | String | The Log Analysis account id the log came from | 
| `app` | String | Application that sent the data | 
| `host` | String | Hostname that sent the data | 
| `id` | String | Unique line identifier | 
| `ingester` | String | Ingestion source of the line | 
| `ip` | String | Originating IP where the data was ingested from | 
| `logtype` | String | The detected log type according to our [supported log sources](https://docs.mezmo.com/docs/log-parsing#parsed-log-sources) | 
| `mac` | String | MAC address of the originating event packet | 
| `mezmo_line_size` | Number | Number of bytes calculated in the line during processing | 
| `noindex` | Boolen | Shows true if an [exclusion rule](https://docs.mezmo.com/docs/excluding-log-lines) prevented the line from being indexed (see note above about fully excluded log lines) | 
| `nostream` | Boolen | Shows true if a streaming exclusion rule prevented the line from being forwarded | 
| `retention` | Number | Retention time in days set for the log line if it matches a [variable retention](https://docs.mezmo.com/docs/variable-retention) rule | 
| `tags` | Array | Tags added to the request query parameters that contained the event | 
{% /table %}

### Examples

#### Ingested log from a Linux OS

{% code %}
{% tab language="json" %}
{
  "message": {
    "_file": "/var/log/syslog",
    "_ipremote": "10.10.129.13",
    "_line": "Oct 20 19:34:48 ubuntu-s-1vcpu-1gb-intel-nyc1-01 systemd[1]: run-docker-runtime\\x2drunc-moby-8cba3a6e51cd96204c067eb66db06d6eac8b77fefad75a7dd60f4c028fd5072d-runc.tMXKDH.mount: Succeeded.",
    "_ts": 1697830488462,
    "logsource": "ubuntu-nyc1-01",
    "message": "run-docker-runtime\\x2drunc-moby-8cba3a6e51cd96204c067eb66db06d6eac8b77fefad75a7dd60f4c028fd5072d-runc.tMXKDH.mount: Succeeded.",
    "pid": 1,
    "program": "systemd"
  },
  "metadata": {
    "query": {
      "account": "8705fc1d41",
      "app": "syslog",
      "host": "ubuntu-nyc1-01",
      "id": "1668622013281333248",
      "ingester": "logdna-agent/2.2.1 (Ubuntu/20.04)",
      "ip": "10.10.0.5",
      "logtype": "syslogline",
      "mac": "7e:2c:e7:c9:7d:c8",
      "mezmo_line_size": 392
    }
  }
}
{% /tab %}
{% /code %}