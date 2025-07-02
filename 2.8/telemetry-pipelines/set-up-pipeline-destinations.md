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

Mezmo Pipeline provides support for multiple types of log data destinations, including Mezmo Log Analysis, cloud storage and monitoring platforms, and analytical tools. If you have an interest in using a pipeline destination not listed here, contact your Account Manager.

All destinations are buffered, meaning that Mezmo Pipelines will not send a set of events until one of the following two conditions is satisfied:

1. The number of events ready to be sent is 500.
2. 300 seconds have elapsed since the first event of a set was received.

If you send data through the Pipeline and it is not showing up in your destination, please check that at least one of the conditions has been satisfied first.

1. Log into [the Mezmo Web App](https://app.mezmo.com/).
2. In the left-hand menu, click **Pipelines**. This will open the **Edit Pipeline** interface.
3. In the left-hand navigation, click **+ New Pipeline**.
4. Enter a name for the Pipeline, then click **Save**.
5. After you have [set up a Pipeline Source,](/telemetry-pipelines/set-up-pipeline-sources) in the **Destinations** column, click **Add**.
6. Select the Destination for your Pipeline log data, and enter the configuration information.
7. To connect your Source and Destination, click the right edge of your Source, and when the and when the blue circle appears, drag the connector from the Source to the Destination until the Destination tile turns blue.

The topic [auto$](/telemetry-pipelines/supported-telemetry-data-destinations) provides a full list of available Destinations and their configuration instructions.

## Video Overview

{% video videoId="799543815" provider="vimeo" %}
{% /video %}