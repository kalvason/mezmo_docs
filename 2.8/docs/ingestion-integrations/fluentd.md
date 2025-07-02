---
type: page
title: Fluentd
listed: true
slug: fluentd
description: Mezmo provides an integration to stream, aggregate, and gain insights from Fluentd logs
index_title: Fluentd
hidden: 
keywords: 
tags: 
---

Mezmo has developed a plugin to send your Fluentd logs to Mezmo. For more detailed information regarding the Fluentd plugin and configuration options, check out our [Github repo](https://github.com/logdna/fluent-plugin-logdna).

## Set Up FluentD Log Ingestion

Follow the instructions in the Mezmo Web App to set up FluentD log ingestion using your Mezmo ingestion key.

1. Log in to the [Mezmo Web App](https://app.mezmo.com).
2. In the bottom section of the left-hand navigation, click **Help**.
3. Select **Add Log Sources**. 
4. Under Via platform, click **FluentD**.
5. Follow the instructions to set up FluentD log ingestion.
Note that your ingestion key is automatically inserted into the configuration code.

## Using FluentD to Tail Logs

Add code to `td-agent.conf`.

{% code %}
{% tab language="none" %}
<source>
  @type tail
  path C:\tmp\*.log    #change to any path
  pos_file C:\tmp\httpd-access.log.pos    #change to any temp path as needed
  tag tail    #could be any tag
  <parse>
    @type none
  </parse>
</source>
{% /tab %}
{% /code %}