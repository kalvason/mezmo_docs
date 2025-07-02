---
type: page
title: FluentD
listed: true
slug: fluentd-pipeline-source
description: 
index_title: FluentD
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/fluentid-pipeline-source#description)

You can stream FluentD logs and metrics to Mezmo Pipelines.

## [Configuration](https://docs.mezmo.com/docs/fluentid-pipeline-source#configuration)

To send your FluentD data to a Mezmo Pipeline, you will need to edit the `Output` section of the FluentD configuration file as shown in this example:

{% code %}
{% tab language="none" %}
# Modify the match criteria to be more specific if needed.
# Modify the endpoint to include your pipeline_id.
# Modify the headers authorization key to match the key generated from the pipeline source.

# The FluentD source decoding method in your pipeline should be set to ndjson.

  <match **>
    @type http
    @id   http1
    endpoint https://pipeline.mezmo.com/v1/<pipeline_id>
    open_timeout 2
    headers {"Authorization": "<key>"}
    content_type json
    <format>
      @type json
    </format>
    <buffer>
      flush_at_shutdown true
      flush_interval 10s
    </buffer>
  </match>
{% /tab %}
{% /code %}

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/fluentid-pipeline-source#mezmo-configuration-options)

{% table %}
| Option | Description | 
| ---- | ---- | 
| Decoding Method | The decoding method to use for converting frames to data events. | 
{% /table %}