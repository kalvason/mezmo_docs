---
type: page
title: Akamai Cloud Monitor
listed: true
slug: akamai-cloud-monitor-logs
description: How to start logging with Akamai Cloud Monitor through Mezmo
index_title: Akamai Cloud Monitor
hidden: 
keywords: 
tags: 
---




Follow the [Cloud Monitor Implementation Guide](https://control.akamai.com/dl/customers/ALTA/Cloud-Monitor-Implementation.pdf) to configure Akamai Cloud Monitor to forward logs to Mezmo.  Use the parameters listed here to set the configuration options.

## Cloud Monitor Data Delivery




{% table %}
| Genera Configuration Option | Parameter | 
| ---- | ---- | 
| **Origin Server Hostname** | `logs.logdna.com` | 
| **HTTP Port** | `443` | 
| **HTTPS Port** | `443` | 
| **Content Provider Code** | Select **812828 - Cloud Monitor to LogDNA**\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nIf this option isn't available, contact Akami Support | 
{% /table %}


{% table %}
| Origin SSL Certificate CN Options | 
| ---- | 
| **Verification Settings** | **Choose Your Own** | 
| **Trust** | **Specific Certificates (pinning)**; | 
| **Match CN/SAN** | `{{Origin-Hostname}}`; | 
| **Hostname/IP** | `logs.logdna.com` | 
| **HTTPS Port** | '443' | 
{% /table %}

## Dynamic Site Accelerator

In your **Dynamic Site Accelerator** configuration, set the **Cloud Monitor Instrumentation** behavior with the these parameters:




{% table %}
|  |  | 
| ---- | ---- | 
| **Cloud Monitor Delivery Hostname** | `logs.logdna.com` | 
| _Data Sets to Include*_ | Specify the datasets for your logs | 
| **Delivery URL Path** | `/akamai/ingest/<Ingestion Key>`\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nUse your Mezmo **Access Key** for '&lt;Ingestion Key&gt;' | 
{% /table %}

{% callout type="info" title="Optional Querystring Parameters" %}
Use querystring parameters to override **hostname**, **app**, or to add **tags**: 

`/akamai/ingest/<Ingestion Key>?hostname=newHost&app=newTest`;
  `/akamai/ingest/<Ingestion Key>?tags=akamai,logdna&app=newTest`;
  `/akamai/ingest/<Ingestion Key>?tags=tag1&hostname=host1`, etc.
{% /callout %}




## How Akamai Logs are Parsed

You can find information for each of your datasets in these log entries:




{% table %}
|  |  | 
| ---- | ---- | 
| **Base Log Line Data** | `meta.*` | 
| **Geographic Data** | `geo.*' | 
| **HTTP 1.0** | `http.*` | 
| **Message Exchange Data** | `http.*` | 
| **Network Data 1.0** | `network.*` | 
| **Network Performance Data** | `netPerf.*` | 
| **Request Header Data** | `reqHdr.*` | 
| **Response Header Data** | `respHdr.*` | 
| **Web Application Firewall Data 2.0** | `waf_2.*` | 
{% /table %}

The information about each dataset and the definition of each field can be found in _Appendix A: Cloud Monitor Default Connectors_ section of [Cloud Monitor Implementation Guide](https://control.akamai.com/dl/customers/ALTA/Cloud-Monitor-Implementation.pdf).

Unless specified, **hostname** is always `http.reqPath` and **app** is always _AkamaiCloudMonitor_.

The log line is formatted using some `http.*` fields as in this example:
`cliIP reqMethod reqPath?reqQuery proto/protoVer status bytes reqCT reqLen respCT respLen UA`

**Notes**:

- `-` is used if the optional field is missing;
- Just `reqPath` is used if there is no `reqQuery`;
- In order to format the line, the fields are joined together using whitespace delimiter in this order:
- `http.cliIP`;
- `http.reqMethod`;
- `http.reqPath?http.reqQuery` or just `http.reqPath`;
- `http.proto/http.protoVer`;
- `http.status`;
- `http.bytes`;
- `http.reqCT`;
- `http.reqLen`;
- `http.respCT`;
- `http.respLen`;
- `http.UA`.





