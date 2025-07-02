---
type: page
title: Set Up Pipeline Destinations
listed: true
slug: set-up-pipeline-destinations
description: 
index_title: Set Up Pipeline Destinations
hidden: 
keywords: 
tags: 
---

Mezmo Pipelines provides support for multiple types of log data destinations, including Mezmo Log Analysis, cloud storage and monitoring platforms, and analytical tools. If you have an interest in using a pipeline destination not listed here, contact your Account Manager.

All destinations are buffered, meaning that Mezmo Pipelines will not send a set of events until one of the following two conditions is satisfied:

1. The number of events ready to be sent is 500.
2. 300 seconds have elapsed since the first event of a set was received.

If you send data through the Pipeline and it is not showing up in your destination, please check that at least one of the conditions has been satisfied first.

## Video Overview

{% video videoId="799543815" provider="vimeo" %}
{% /video %}