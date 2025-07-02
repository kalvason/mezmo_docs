---
type: page
title: Demo Logs
listed: true
slug: demo-logs-source
description: 
index_title: Demo Logs
hidden: 
keywords: 
tags: 
---

## Description

Mezmo provides several types of demo logs for you to use in building and testing your Pipelines. These can be especially useful to make sure that your Processors are accurately transforming and routing your data as expected. 

## Configuration

The demo log sources are ready to use, you only need to choose which option best matches the type of log data you want to test. 

{% callout type="info" title="Data Volume for Demo Sources" %}
The demo logs consistently push between 25Mb-50Mb of data per day.
{% /callout %}

### Configuration Options

{% table widths="205" %}
| Option | Sample | 
| ---- | ---- | 
| env_sensor | Simulated logs from environmental sensors | 
| financial | Simulated logs from financial applications | 
| nginx | Simulated logs from NGINX | 
| json | Simulated JSON logs | 
| apache_common | Simulated common Apache logs | 
| apache_error | Simulated Apache error logs | 
| bsd_syslog | Simulated BSD syslog format logs | 
| syslog | Simulated syslog format logs | 
| http_metrics | Simulated log metrics | 
| generic_metrics | Metrics with vague naming for simulating any source | 
{% /table %}

## Examples

### Environmental Sensor

{% code %}
{% tab language="json" %}
{
  "data": {
    "co": 0.004020215,
    "humidity": 31.60854,
    "light": false,
    "lpg": 0.009137373,
    "motion": false,
    "smoke": 0.016502323,
    "temp": 23.443808
  },
  "device_id": "1c:bf:ce:15:ec:4d",
  "ts": 1680193367.066066
}
{% /tab %}
{% /code %}

### Financial Log

{% code %}
{% tab language="json" %}
{
  "access": {
    "action": "login",
    "name": "Nola Daniel",
    "user_id": "cd356412-78fa-3829-b303-62836d77c62d"
  },
  "buffer": "a5217abb-88b5-4042-9543-f6b830c7c77f",
  "datetime": "2023-03-30T16:24:37.393392918+00:00",
  "device": {
    "id": "dcab649c-a999-410d-bebd-9e7ba3c5bd28",
    "location": [
      -66.875,
      166.553
    ],
    "name": "/dev/sdl",
    "status": "active",
    "vrs": "1.3.4"
  },
  "event": "access"
}
{% /tab %}
{% /code %}

### Nginx Log

{% code %}
{% tab language="none" %}
234.122.140.51 - - [30/Mar/2023:16:26:46 +0000] \"GET / HTTP/1.1\" 401 9609 Mozilla/5.0 (X11; CrOS x86_64 8172.45.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.64 Safari/537.36
{% /tab %}
{% /code %}

### JSON Log

{% code %}
{% tab language="json" %}
{
  "bytes": 8276,
  "datetime": "30/Mar/2023:16:17:52",
  "host": "144.230.103.114",
  "method": "POST",
  "protocol": "HTTP/1.1",
  "referer": "hammes.info",
  "request": "/",
  "status": 200,
  "user-identifier": "uschmeler"
}
{% /tab %}
{% /code %}

### Apache Common

{% code %}
{% tab language="none" %}
218.110.40.3 - - [30/Mar/2023:16:29:42 +0000] \"PUT /assets780054b0e33b506276833d1d0a50ccb HTTP/1.1\" 200 9241
{% /tab %}
{% /code %}

### Apache Error

{% code %}
{% tab language="none" %}
[Thu Mar 30 16:32:11 2023] [ERROR] [pid 14495:tid 31372] [client 247.233.28.3:6329] mod_jk child workerEnv in error state 6
{% /tab %}
{% /code %}

### BSD Syslog

{% code %}
{% tab language="none" %}
<125>Mar 30 16:32:57 koelpin.biz sshd[9148]: authentication failure; logname= uid=0 euid=0 tty=NODEVssh ruser= rhost=troi.bluesky-technologies.com user=root
{% /tab %}
{% /code %}

### Syslog

{% code %}
{% tab language="none" %}
<4>3 2023-03-30T16:34:30.404Z keebler.info bhermiston 4859 ID710 - authentication failure; logname= uid=0 euid=0 tty=NODEVssh ruser= rhost=061092085098.ctinets.com
{% /tab %}
{% /code %}

#### HTTP Metrics

{% code %}
{% tab language="json" %}
{
  "kind": "incremental",
  "name": "sent_kilobytes_total",
  "namespace": "http.server",
  "tags": {
    "hostname": "host1.example.com",
    "method": "POST",
    "path": "/example"
  },
  "value": {
    "type": "counter",
    "value": 2680
  }
}
{% /tab %}
{% /code %}

#### Generic Metrics

{% code %}
{% tab language="json" %}
{
  "kind": "incremental",
  "name": "counter1",
  "namespace": "namespace1",
  "tags": {
    "field1": "value2",
    "field2": "value9",
    "field3": "value3"
  },
  "value": {
    "type": "counter",
    "value": 1
  }
}
{% /tab %}
{% /code %}