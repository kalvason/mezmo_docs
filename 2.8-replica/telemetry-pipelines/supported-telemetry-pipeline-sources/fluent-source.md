---
type: page
title: FluentD and FluentBit
listed: true
slug: fluent-source
description: 
index_title: FluentD and FluentBit
hidden: 
keywords: 
tags: 
---


## [Description](https://docs.mezmo.com/docs/fluentid-pipeline-source#description)

You can stream FluentD and FluentBit logs and metrics to Mezmo Pipelines using HTTP output plugins for SaaS pipelines, and Forward output plugins for [Mezmo Edge Pipelines](/mezmo-edge/mezmo-edge-pipelines-for-local-data).

## [Configuration](https://docs.mezmo.com/docs/fluentid-pipeline-source#configuration)


#### FluentD

To send your FluentD data to a Mezmo Pipeline, add to a `v1`  config file, a `match`  with the `http`  output plugin configured as follows:

{% code %}
{% tab language="bash" %}

## Modify the match criteria to be more specific if needed.

## Modify the endpoint to include your pipeline_id.

## Modify the headers authorization key to match the key generated from the pipeline source.


## The FluentD source decoding method in your pipeline should be set to ndjson.

&lt;match **&gt;
@type http
@id   http1
endpoint https://pipeline.mezmo.com/v1/&lt;YOUR ROUTE ID&gt;
open_timeout 2
headers {"Authorization": "&lt;YOUR GENERATED ACCESS KEY&gt;"}
&lt;format&gt;
@type json
&lt;/format&gt;
&lt;buffer&gt;
flush_at_shutdown true
flush_interval 10s
&lt;/buffer&gt;
&lt;/match&gt;
{% /tab %}
{% /code %}

Note that, while the `format` says `json` here, because the setting `json_array`[defaults to `false`](https://docs.fluentd.org/output/http#content_type) , FluentD will be emitting `json`  objects without the enclosing array. Therefore, **Decoding Method** should be set to `ndjson` .


#### FluentBit

FluentBit can be configured to send data to any Mezmo Pipeline HTTP source. Please see the examples for both Classic and YAML configuration below, making the appropriate substitutions for your source path and key.

For YAML, add a new output in under the pipeline group:

{% code %}
{% tab language="yaml" %}
pipeline:
outputs:
- name: http
match: '*'
host: 'pipeline.mezmo.com'
uri: '/v1/&lt;YOUR ROUTE ID&gt;'
header: 'Authorization: &lt;YOUR GENERATED ACCESS KEY&gt;'
tls: 'on'
port: 443
format: 'json_lines'
{% /tab %}
{% /code %}

The output is added to classic configurations by adding an `Output` block to the top level as follows:

{% code %}
{% tab language="bash" %}
[output]
name http
match *
host pipeline.mezmo.com
uri &lt;URL PATH FROM YOUR SOURCE CONFIGURATION&gt;
header "Authorization: &lt;YOUR GENERATED ACCESS KEY&gt;"
tls on
port 443
format json_lines
{% /tab %}
{% /code %}

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/fluentid-pipeline-source#mezmo-configuration-options)

{% table widths="" %}

{% table %}
| Option | Description | 
| ---- | ---- | 
| Decoding Method | The decoding method to use for converting frames to data events. | 
{% /table %}

{% /table %}