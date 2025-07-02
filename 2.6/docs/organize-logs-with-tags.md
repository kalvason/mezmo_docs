---
type: page
title: Organize Logs With Tags
listed: true
slug: organize-logs-with-tags
description: 
index_title: Organize Logs With Tags
hidden: 
keywords: 
tags: 
---

Tagging is a way to organize your data. While we automatically parse your log data and make it available, using tags can give you [advanced filtering](/docs/search-and-filter). Use tags to filter logs from searches or only show certain logs in the log viewer. 

## Add Tags

These instructions are for[ Agent V2](https://github.com/logdna/logdna-agent-v2/tree/master/docs#options). 

### Windows

{% code %}
{% tab language="bash" %}
http:
  params:
    tags: windows_agent_mezmo
{% /tab %}
{% /code %}

### Helm

Tags can be added during installation or in the configuration file.

{% code %}
{% tab language="yaml" %}
logdna:
    tags: green, yellow, blue
{% /tab %}
{% /code %}

{% code %}
{% tab language="yaml" %}
helm install --set logdna.key=$LOGDNA_INGESTION_KEY -n my-namespace --create-namespace my-release logdna/agent
{% /tab %}
{% /code %}

### Kubernetes

{% code %}
{% tab language="yaml" %}
name: LOGDNA_TAGS
value: green, yellow, blue
{% /tab %}
{% /code %}

### Linux

{% code %}
{% tab language="bash" %}
LOGDNA_TAGS=production, bananas
{% /tab %}
{% /code %}

## View Tags

You can view your tags in the Mezmo UI. 

1. In the Mezmo Viewer, go to the top bar and click **Tags.** You'll see a list of all your tags.
2. You can also click on a log to see any attached tags.

{% image url="https://uploads.developerhub.io/prod/2KW7/h7h9mh93yux9ar55zjtpcudy12ygujc16y3tb6unazg9bkapxrgj9b2qo3lliwae.png" caption="Mezmo UI logs shows the agent-v2, stage, us-east-1, and aws tags." mode="responsive" height="1148" width="1676" %}
{% /image %}