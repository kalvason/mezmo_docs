---
type: page
title: HTTP Source for Mezmo Edge
listed: true
slug: http-source-mezmo-edge
description: 
index_title: HTTP Source for Mezmo Edge
hidden: 
keywords: 
tags: 
---


## Description

You can configure any source to send data via a RESTful POST to a Mezmo Edge Pipeline.

{% callout type="success" title="Parsing Data after Ingestion" %}
When using the HTTP source, your content must be encoded appropriately, and packaged in a way that enables it to be parsed after ingestion. Structured formats, such as JSON, do not require additional parsing unless you want to further parse a specific value within the JSON.
{% /callout %}

You would typically use an HTTP request as a Source when the type of Source you want to send data from is not supported. For example, you may want to send  and process data from an uncommon open source application.  As long as you're able to use a RESTful POST transport to send the data to an endpoint, you can send the data into the Pipeline.

## Configuration

This Source requires an allocated port that you will forward the data to. You must use a port that has been configured within your Edge instance during set up.

{% callout type="info" title="Default Edge Port Ranges" %}
The default Edge port range is 8000-8010, unless you modified it during set up.
{% /callout %}

### Configuration Options

{% table %}

{% table %}
| **Setting** | **Description** | 
| ---- | ---- | 
| **Title** | A name for your source. | 
| **Description** | A short description of the source. | 
| **Port** | The port number to listen on within the Edge instance. | 
{% /table %}

{% /table %}