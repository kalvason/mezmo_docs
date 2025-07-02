---
type: page
title: Syslog Source for Mezmo Edge
listed: true
slug: syslog-source-for-mezmo-edge
description: 
index_title: Syslog Source for Mezmo Edge
hidden: 
keywords: 
tags: 
---


## Description

You can send syslog events and data to Mezmo Edge Pipelines directly through a specified port on the Edge instance.

## Configuration

Add the [auto$](/telemetry-pipelines/syslog-over-http-pipeline-source)  Source to your Edge Pipeline. This Source will automatically convert syslogs to parsed logs when ingested.

An API key is not required, and the connection is not protected with encryption. This is intended for use within your own network and isolated from the wide area network.

{% callout type="info" title="Edge Port Ranges" %}
The Edge instances have default port ranges of 8000-8010. You can add port numbers if required.

Each Source in Edge requires a unique port number in order to receive data. The port number you use must fall within the range that is set upon deployment.
{% /callout %}