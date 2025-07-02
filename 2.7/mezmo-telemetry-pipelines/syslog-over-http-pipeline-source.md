---
type: page
title: Syslog over HTTP
listed: true
slug: syslog-over-http-pipeline-source
description: 
index_title: Syslog over HTTP
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/syslog-over-http-pipeline-source#description)

## 
You can send Syslog events and data to Mezmo Pipelines through an HTTP endpoint.

{% callout type="info" title="Why don't we allow standard syslog?" %}
The default syslog port is unavailable due to the lack of inherent security. HTTP forwarding is now a common practice for syslog via TLS to protect from packet sniffing and plain text transmission.
{% /callout %}

## [Configuration](https://docs.mezmo.com/docs/syslog-over-http-pipeline-source#configuration)

Use the standard HTTP endpoint for the configuration. Ensure that the encoding matches the configuration of your source.

{% callout type="info" title="Discrete Parsing Process Required" %}
You must use a discrete parsing processor after the source in order to properly ingest the data and make it accessible to subsequent processors in a pipeline.
{% /callout %}

This example of an rsyslog configuration illustrates using a defined template to allow inclusion of the API key with the `omhttp` [output module documented here](https://www.rsyslog.com/doc/v8-stable/configuration/modules/omhttp.html).

{% code %}
{% tab language="bash" %}
module(load="omhttp")
template(name="tpl1" type="string" string="{\"type\":\"syslog\", \"host\":\"%HOSTNAME%\"}")
action(
    type="omhttp"
    server="pipeline.app.mezmo.com"
    serverport="443"
     httpheaders=[
        "Authorization: s_<TOKEN>"
    ]
    template="tpl1"
    action.resumeRetryCount="100"
    batch="on"
    batch.format="jsonarray"
    batch.maxsize="10"
)
{% /tab %}
{% /code %}

{% callout type="info" title="Discrete Parsing Process Required" %}
You must use a discrete parsing processor after the source in order to properly ingest the data and make it accessible to subsequent processors in a pipeline.
{% /callout %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Decoding Method | The decoding method to use to convert frames to data events. | 
{% /table %}