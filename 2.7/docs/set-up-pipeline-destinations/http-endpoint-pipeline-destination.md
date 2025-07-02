---
type: page
title: HTTP Endpoint
listed: true
slug: http-endpoint-pipeline-destination
description: 
index_title: HTTP Endpoint
hidden: 
keywords: 
tags: 
---

## Description

You can send your Mezmo Pipeline log data to any HTTP endpoint.

## Configuration Options

{% table %}
| Option | Description | 
| ---- | ---- | 
| End-to-End Acknowledgement | Enable this option to receive verification that log data is being received by the HTTP endpoint. | 
| URI | The full URI for HTTP requests. This should include the protocol and host, but can also include the port, path, and any other valid part of a URI. | 
| Encoding | The type of encoding to apply to the data. | 
| Compression | The compression to apply to the encoded log data before sending it to the endpoint. | 
| Authentication Strategy | The strategy to use for authentication to the HTTP endpoint. | 
| HTTP Headers | An array of key/value objects for the headers to be sent with the request. | 
{% /table %}