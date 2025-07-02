---
type: page
title: HTTP
listed: true
slug: http-pipeline-source
description: 
index_title: HTTP
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/http-pipeline-source#description)

You can configure any HTTP source to send logs to the Memzo Pipeline. You would typically use an HTTP request as a source when you want to read data in from a server, cluster, or cloud provider to examine the tasks being completed on those entities, paired with their response. These responses can be processed within the pipeline to [remove](/docs/remove-fields-pipeline-processor) or [encrypt](/docs/encrypt-field-pipeline-processor) any sensitive data they contain before sending them to other tools for application performance monitoring, log analysis, or security information and event monitoring. The topic [auto$](/docs/pipeline-architecture-HTTP-endpoint) provides a basic example of how to set up your HTTP endpoint Source and typical Processors you would use.

{% callout type="info" title="Use Buffering for Log Requests" %}
If you use an individual request per log, you will quickly exceed your network capacity, so we recommend using a buffering solution.
{% /callout %}

## [Configuration](https://docs.mezmo.com/docs/http-pipeline-source#configuration)

In the HTTP source configuration, use the pipeline data endpoint and configure the appropriate content type in your request. You must ensure that the API key is included in the header with the configuration for `Authorization: s_<unknown>` .

{% callout type="info" title="Parsing Data after Ingestion" %}
When using the HTTP source, your content must be both encoded appropriately and packaged in way that enables it to be parsed after ingestion. You must also use a [auto$](/docs/parse-pipeline-processor) explicitly after ingestion in order to make use of any structured data.
{% /callout %}

### [Mezmo Configuration Options](https://docs.mezmo.com/docs/http-pipeline-source#mezmo-configuration-options)

The topic [auto$](/docs/pipeline-architecture-HTTP-endpoint) includes more information how to configure and test your HTTP endpoint source.

{% table %}
| Setting | Description | 
| ---- | ---- | 
| **Title** | A name for your source. | 
| **Description** | A short description of the source. | 
| Decoding Method | The decoding method to use to convert frames to data events | 
| **Access Key Management** | 1. Click **Create new key** to generate an access key.\n2. Enter a **Title** for the key.\n3. Click **Create**.\n\n\nMake sure to copy the Access Key and note the Ingestion URL, which should resemble `https://pipeline.mezmo.com/v1/%YOUR PIPELINE ID%.` | 
{% /table %}