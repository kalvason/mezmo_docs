---
type: page
title: Splunk HEC
listed: true
slug: splunk-hec-pipeline-source
description: 
index_title: Splunk HEC
hidden: 
keywords: 
tags: 
---

## Description

You can send events from the Splunk HTTP Event Collector to Mezmo Pipelines. Splunk HEC was created so Splunk users could send HTTP data directly and securely to Splunk. Typically you would use Splunk HEC as a source because you want your observability-related events to be redirected over to your SIEM tool for further processing. By first sending this data through Pipeline processors, you can remove fields, parse the JSON content of an HTTP response into an integer or key:value pair, and overall reduce the amount and cost of data that you are sending for further analysis. 

## Configuration

The Spunk HEC forwarder requires an `outputs.conf` configuration to forward events to the Mezmo Pipeline. This uses a TCP configuration to send the events. The [Splunk HEC configuration file reference](https://docs.splunk.com/Documentation/Splunk/9.0.3/Admin/Outputsconf) contains more information for setting this up, including specific information for HEC versions.