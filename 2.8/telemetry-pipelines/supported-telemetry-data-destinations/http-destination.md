---
type: page
title: HTTP Endpoint
listed: true
slug: http-destination
description: 
index_title: HTTP Endpoint
hidden: 
keywords: 
tags: 
---

## [Description](https://docs.mezmo.com/docs/http-endpoint-pipeline-destination#description)

You can send your Mezmo Pipeline log data to any HTTP endpoint.

## [Configuration Options](https://docs.mezmo.com/docs/http-endpoint-pipeline-destination#configuration-options)

### Basic

Basic configuration options are exposed by default.

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

### Advanced

Advanced options can be reached by expanding the lower accordion section within the destination page.

{% table %}
| Option | Description | 
| ---- | ---- | 
| Payload size | The maximum number of uncompressed bytes when batching data to send to the destination. | 
| Timeout seconds | The number of seconds to wait for a response until timing out. | 
| HTTP Method | If a method other than POST is desired, select any of the standard HTTP request type options including PUT, PATCH, DELETE, GET, HEAD,  OPTIONS, TRACE | 
| Payload Prefix | Add characters to the request payload if needed. \n\n\n\n_If added a suffix is also required._ | 
| Payload Suffix | Used in conjunction with the Prefix option for enclosing the payload.\n\n\n\n_If added a prefix is also required._ | 
| Proxy Settings | When enabled, allows for proxies to be used to send data to the specified destination. | 
| HTTP(S) Endpoint | The proxy endpoint to use for sending traffic when Proxy Settings are enabled. | 
| Hosts to bypass | The list of hosts to bypass when Proxy Settings are enabled. Can be a domain name, IP address, or CIDR block. Supports dots (.) in domain names and wildcards (*) to match on all hosts. | 
| TLS Protocols | A list of the ALPN protocols to attempt, in order of how they are entered. | 
| Request Limit | The maximum number of requests to try within the specified request duration. \n\n\n\n_The default value is_ `9.223372036854776e+18` | 
| Duration Seconds | The amount of time over which to \n\n\n\n_The default duration is 1 second._ | 
{% /table %}