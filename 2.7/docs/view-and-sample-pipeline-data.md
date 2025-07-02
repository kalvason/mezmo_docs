---
type: page
title: View Pipeline Data
listed: true
slug: view-and-sample-pipeline-data
description: 
index_title: View Pipeline Data
hidden: 
keywords: 
tags: 
---

You can view the data flowing between segments of your pipeline by using a **Pipeline Tap**. 

## Insert a Pipeline Tap

1. Log in to [the Mezmo Web App](https://app.mezmo.com).
2. Click **Pipelines**.
3. Select the Pipeline where you want to insert a Pipeline Tap.
4. In that Pipeline, hover on the right edge of a Source node until it turns blue, then click to open the **Pipeline Tap** drawer.
5. Enter the number of log events you want to view in the Pipeline Tab, then click **Play**. You will see the data flowing from that Source or Processor begin to stream in the Pipeline Tap drawer based on the number of Log Events you set.
6. Use the filter fields at the top of the tap to select specific events to view. 

{% callout type="info" title="Deployed Pipelines Only" %}
You can only insert a Data Tap on a segment of a deployed Pipeline.
{% /callout %}

## Video Overview

{% video videoId="30ba3d9493264ea681b622d9369c4b7c" provider="loom" %}
{% /video %}